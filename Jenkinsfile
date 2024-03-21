pipeline {
    agent any
    stages {
        stage('Validar Existencia de index.html') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/Troon200/trabajo-final.git'
                    def exists = fileExists("index.html")
                    if (exists) {
                        echo "El archivo index.html existe en el repositorio."
                    } else {
                        error "El archivo index.html no existe en el repositorio."
                    }
                }
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'sonar';
                    withSonarQubeEnv() {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
        
        stage('Quality Gate') {
            steps {
                script {
                    sleep time: 100, unit: 'SECONDS'
                    timeout(time: 1, unit: 'HOURS') {
                        waitForQualityGate abortPipeline: true
                    }
                    echo "El 'Quality Gate' ha sido superado exitosamente."
                }
            }
        }
        
        stage('Despliegue Exitoso') {
            steps {
                echo "El despliegue fue exitoso."
            }
        }
        
        stage('OWASP ZAP Scan') {
            steps {
                script {
                    sh "docker exec -it zap zap.sh -deamon -quickurl http://172.18.0.5:80 -quickout /tmp/resultados.html"
                }
            }
        }
    }
}
