pipeline {

  agent any
  
  
  environment {
    PROJECT_ID = 	'playground-s-11-e9f09a75'
    CLUSTER_NAME = 'cluster-1'
    LOCATION = 'us-central1-c'
    CREDENTIALS_ID = 'kubernetes'
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
  }
}
    post {
            success {
                slackSend "Build deployed successfully - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"

            }
        }
    
    
