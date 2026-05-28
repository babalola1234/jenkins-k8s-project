pipeline {
  agent { label 'terraform-node' }

  parameters {
    choice(
      name: 'action',
      choices: ['apply','delete'],
      description: 'Select the action to deploy'
    )
  }

  stages {
    stage('Deploy to K8s') {
      steps {
        withCredentials([file(credentialsId: 'credentials', variable: 'KUBECONFIG')]) {
          sh '''
            echo "Using kubeconfig at: $KUBECONFIG"
            ls -l $KUBECONFIG
            kubectl --kubeconfig=$KUBECONFIG ${action} -f mypod.yml
          '''
        }
      }
    }
  }
}

