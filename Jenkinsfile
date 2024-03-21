pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "3"
            }
        }
        stage('Test') {
            steps {
                echo "2"
            }
        }
        stage('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Troon200/trabajo-final.git'
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
        stage('OWASP ZAP Scan') {
            steps {
                script {
                    sh "docker exec -it zap zap.sh -deamon -quickurl http://172.18.0.5:80 -quickout /tmp/resultados.html"
                }
            }
        }
    }
}
