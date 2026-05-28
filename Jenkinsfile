pipeline {
  agent { label 'terraform-node' }
    parameters {
        choice(
            name: 'action',
            choices: ['apply','delete'],
            description: 'Select the anyone option to deploy'
        )
    }

  stages {
    stage('Deploy to K8s') {
      steps {
        withCredentials([file(credentialsId: 'credentials', variable: 'KUBECONFIG')]) {
          sh 'kubectl --credentials $KUBECONFIG ${action} -f mypod.yml'
        }
      }
    }
	}
	post {
    success {
      echo "Pipeline completed successfully"
    }
    failure {
      echo "Pipeline failed"
    }
  }
}
