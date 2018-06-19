node {
  stage('checkout code') {
    checkout scm
  }
}
node{
  stage('npm install') {
    nodejs(configId: '28aade4d-b00c-461a-9d8a-d0fd054805da', nodeJSInstallationName: 'NodeJS 8.11.3') {
      sh 'npm --version'
      sh 'node --version'
      sh 'npm install'
    }
  }
}

node {
  stage('Package app') {
    nodejs('NodeJS 8.11.3') {
      sh 'npm run  package:apps'
    }
  }  
}

stage('Deploy') {
input message: 'Deploy to Dev?'
  node {
    withMaven(maven: 'Maven 3.5.3') {
        sh 'mvn bb:provision -Premote-dev'
    }
  }   
}
