pipeline {
  agent any

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
            sh 'echo $BUILD_NUMBER'
            sh 'sudo docker login -u jtran33 -p Jasperispuppy3355?'
            sh 'sudo docker build -t jtran33/jtran51_hw2_645:$BUILD_NUMBER .'
        }
      }
    }
    
    stage('Push to Docker Hub') {
      steps {
        script {
            sh 'sudo docker push jtran33/jtran51_hw2_645:$BUILD_NUMBER'
          }
        }
      }
    
    stage('Deploy to Rancher') {
      steps {
        script {
          sh 'kubectl set image deployment/swe645_hw_pipeline swe645_hw_pipeline=jtran33/jtran51_hw2_645:$BUILD_NUMBER'
        }
      }
    }
  }
}