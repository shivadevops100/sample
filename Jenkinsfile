pipeline{
    agent {
        label 'k8s'
    }
    environment {
        KUBECONFIG = '/home/ubuntu/.kube/kind-config-kind'

    }
    stages{
        stage('clone repo'){
            steps{
            git 'https://github.com/shivadevops100/sample.git'
        }
    }
        stage('Build image'){
            steps{
                sh 'docker build -t shiva .'
            }
        }
        stage('Tag and push to Hub'){
            steps{
               
                sh 'docker tag shiva shivakoppera/shiva:"${BUILD_NUMBER}"'
                sh 'docker push shivakoppera/shiva:"${BUILD_NUMBER}"'
            }
        }
        stage('Deployment'){
            steps{
            
               sh 'echo $KUBECONFIG'
                sh 'kubectl set image deployment/nginx shiva="${BUILD_NUMBER}"'
            }
        }
        
        
    }
      
  }
