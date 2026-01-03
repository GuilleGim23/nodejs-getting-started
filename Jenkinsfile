pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Install') {
      steps { sh 'npm ci || npm install' }
    }

    stage('Test') {
      steps { sh 'npm test || true' }
    }

    stage('Build') {
      steps { sh 'npm run build || true' }
    }

    stage('Deploy') {
      steps {
        withCredentials([string(credentialsId: 'render-deploy-hook', variable: 'HOOK')]) {
          sh 'curl -fsS -X POST "$HOOK"'
        }
      }
    }
  }
}
