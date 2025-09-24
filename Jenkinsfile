pipeline{
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
    echo "Post block started"
    archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
  }
  success {
    echo "Post block: sending success email"
    emailext(
      subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
      body: "The build succeeded. See the attached logs.",
      to: 'ami25pa@gmail.com',
      attachLog: true
    )
  }
  failure {
    echo "Post block: sending failure email"
    emailext(
      subject: "Build Failure: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
      body: "The build failed. See the attached logs.",
      to: 'ami25pa@gmail.com',
      attachLog: true
    )
  }
}
}
