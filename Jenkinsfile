pipeline {
  agent any

  stages {

    stage('Checkout Code') {
      steps {
        checkout scm
      }
    }

    stage('Approval to Deploy to On-Prem') {
      steps {
        input message: 'Approve deployment to ON-Prem (Main)?'
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
          kubectl --context gke_learning-gcp-stage_us-central1-a_oci-oke \
            apply -f jenkins-deploy/
        '''
      }
    }
  }
}

