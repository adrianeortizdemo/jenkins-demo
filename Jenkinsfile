pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // Pull your code from whatever SCM this repo lives in
        checkout scm
      }
    }

    stage('Setup Python') {
      steps {
        // Create & activate the same venv you used locally
        sh 'python3 -m venv .venv'
        sh '.venv/bin/pip install --upgrade pip'
        sh '.venv/bin/pip install -r requirements.txt'
      }
    }

    stage('Run Tests') {
      steps {
        // Run pytest and output JUnit XML for Jenkins to consume
        sh '.venv/bin/pytest --junitxml=report.xml'
      }
      post {
        always {
          // Publish test results in Jenkins’ Test Results
          junit 'report.xml'
        }
      }
    }
  }
}
