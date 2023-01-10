//test
pipeline {                   
  agent {
    label 'jenkins-build-node'
  }
  stages {
    stage('Generate Token') {
      steps {
        sh '''
             cd /home/deploy/jenkins/workspace/
             token=$(ruby generate-jwt-token.rb)
            '''

      }
    }
    stage('Git Clone') {
      steps {
        sh  '''
             rm -rf bulletin-board/
             git clone https://x-access-token:$token@github.com/Jijo070/bulletin-board
             ls -ltra && cd bulletin-board/ && ls -ltra
            '''
      }
    }
  }
}
