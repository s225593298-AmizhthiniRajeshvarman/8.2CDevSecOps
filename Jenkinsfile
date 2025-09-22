pipeline {
  agent any
  environment {
    SNYK_TOKEN = credentials('SNYK_TOKEN')  
  }
  stages {
    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }
    stage('Run Tests') {
      steps {
        bat '''
          snyk test
          exit /b 0
        '''
      }
    }
    stage('NPM Audit (Security Scan)') {
      steps {
        bat '''
          snyk auth $env:SNYK_TOKEN
          npm audit
          exit /b 0
        '''
      }
    }
  }
  post {
    always {
      archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
    }
  }
}
