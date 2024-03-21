node {
  stage('SCM') {
    git branch: 'main', url: 'https://github.com/Troon200/trabajo-final.git'
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'SonarScanner';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
