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
        stage('Deploy') {
            steps {
                echo "1"
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
    }
}

