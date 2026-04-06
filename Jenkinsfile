pipeline {
 agent { label 'selvaa' }

 stages {

  stage('Clone Repository') {
   steps {
    git branch: 'main',
    url: 'https://github.com/Selva-git-22/Jenkins-CICD.git'
   }
  }

  stage('Clean Workspace') {
   steps {
    sh '''
    rm -rf node_modules
    rm -f package-lock.json
    '''
   }
  }

  stage('Install Dependencies') {
   steps {
    sh 'npm install'
   }
  }

  stage('Build Website') {
   steps {
    sh 'npm run build'
   }
  }

  stage('Remove Old Container') {
   steps {
    sh '''
    docker stop jenkins-demo || true
    docker rm jenkins-demo || true
    docker rmi jenkins-demo || true
    '''
   }
  }

  stage('Build Docker Image') {
   steps {
    sh 'docker build -t jenkins-demo .'
   }
  }

  stage('Run Container') {
   steps {
    sh 'docker run -d -p 80:80 --name jenkins-demo jenkins-demo'
   }
  }

 }
}
