pipeline {
  agent any
  environment {
	DOCKERHUB_PASS= credentials('docker-pass') 
  }
  stages {
    stage('Checkout GitHub Repository') {
      steps {
        checkout scm
      }
    }
    
    stage('Build Docker Image') {
      steps {
        script {
            sh 'rm -rf *.war'
            sh 'jar -cvf jtran51_assignment1_part2.war -C src/ .'
            sh 'echo $BUILD_TIMESTAMP'
            sh '$DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            def customImage = docker.build("jtran33/jtran51_hw2_645:$BUILD_TIMESTAMP")
        }
      }
    }
    
    stage('Push to Docker Hub') {
      steps {
        script {
            sh 'sudo docker push jtran33/jtran51_hw2_645:$BUILD_TIMESTAMP'
          }
        }
      }
    
    stage('Deploy to Rancher') {
      steps {
        script {
          sh 'kubectl set image deployment/swe645_hw_pipeline swe645_hw_pipeline=jtran33/jtran51_hw2_645:${BUILD_TIMESTAMP} -n pipeline'
        }
      }
    }
  }
}