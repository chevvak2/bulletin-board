pipeline {                   
  agent {
    label 'jenkins-build-node'
  }
  triggers {
      GenericTrigger(
          genericVariables: [
              [key: 'ref', value: '$.ref'],
              [key: 'html_url', value: '$.repository.html_url'],
          ],

          causeString: 'Triggered on $html_url/$ref',

          token: 'jenkins-webhook-jhgdd2wha12kskas43d', 

          printContributedVariables: true,
          printPostContent: true,

          silentResponse: false,

          regexpFilterText: '$html_url/$ref',

          regexpFilterExpression: 'https://github.com/(jijo070)/(bulletin-board)/refs/heads/(master|main)'
      )
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
