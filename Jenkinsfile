pipeline {
  agent any

  stages {

    stage('Checkout Code') {
      steps {
        checkout scm
      }
    }

    stage('Deploy to On-Prem (MAIN)') {
      steps {
        sh '''
          kubectl --context kubernetes-admin@kubernetes \
            apply -f jenkins-deploy/
        '''
      }
    }

    stage('Approval to Deploy to Cloud') {
      steps {
        input message: 'Approve deployment to CLOUD (OKE)?'
      }
    }

    stage('Deploy to Cloud (OKE)') {
      steps {
        sh '''
          kubectl --context gke_learning-gcp-stage_us-central1-a_oci-cluster-2 \
            apply -f jenkins-deploy/
        '''
      }
    }
  }
}

