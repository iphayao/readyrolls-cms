pipeline {
    agent {
        kubernetes {
          yamlFile 'k8s/KubernetesPod.yaml'
        }
    }
    stages {
        stage('Build Image') {
            steps {
                container('docker') {
                    sh 'docker build -t localhost:32000/strapi .'
                }
            }
        }
        stage('Push Image') {
            steps {
                container('docker') {
                     sh 'docker push localhost:32000/strapi'
                }
            }
        }
        stage('Deployment') {
            steps {
                container('kubectl') {
                     sh 'kubectl delete -f deploy/deployment.yaml -n strapi --ignore-not-found=true'
                     sh 'kubectl apply -f deploy/deployment.yaml -n strapi'
                }
            }
        }
    }
}
