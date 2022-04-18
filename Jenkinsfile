pipeline {
  agent {
    docker {
     image 'node:6-alpine'
     args '-p 3000:3000'
    }
  }
  environment {
    CI = 'true'
    HOME = '.'
    npm_config_cache = 'npm-cache'
  }
  stages {
    stage('Version') {
        steps {
            nodejs(nodeJSInstallationName: "node") {
                sh 'node -v'
            }
        }
    }
    stage('Install Packages') {
      steps {
        nodejs(nodeJSInstallationName: "node"){
        sh 'npm install'}
      }
    }
    stage('Test and Build') {
      parallel {
        stage('Run Tests') {
          steps {
            nodejs(nodeJSInstallationName: "node"){
            sh 'npm run test'}
          }
        }
        stage('Create Build Artifacts') {
          steps {
              nodejs(nodeJSInstallationName: "node"){
            sh 'npm run build'}
          }
        }
      }
    }
    }
}
