pipeline {

  agent any
  
  
  environment {
    PROJECT_ID = 	'euphoric-grin-335112'
    CLUSTER_NAME = 'cluster-1'
    LOCATION = 'us-central1-b'
    CREDENTIALS_ID = 'project'
  }

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/Nurmukhamed02/project-kube-cicd.git', branch:'main'
      }
    }

    stage('deploytokubernetes') {
      steps {
        step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
    
        }
      }
    stage('slack') {
      steps {
        slackSend color: 'good', message: 'Build deployed successfully', tokenCredentialId: 'slack-bot-token'

      }
    } 
  }
}
   
