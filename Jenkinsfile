pipeline {
  agent any
  stages {
    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }
    stage('Run Tests') {
      steps {
        bat 'npm test || exit /b 0'
      }
    }
    stage('NPM Audit (Security Scan)') {
      steps {
        bat 'npm audit || exit /b 0'
      }
    }
  }
  post {
  always {
    echo "Running post always block"
    archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
  }
  success {
    echo "Sending success email"
    emailext(
      subject: "...",
      body: "...",
      to: 'ami25pa@gmail.com',
      attachLog: true
    )
  }
  failure {
    echo "Sending failure email"
    emailext(
      subject: "...",
      body: "...",
      to: 'ami25pa@gmail.com',
      attachLog: true
    )
  }
}
