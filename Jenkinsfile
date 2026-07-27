pipeline {
  agent any
    stages {
        stage('Build and Push Image') {
            steps {
                sh '''
                    docker build -t treeone008/ktcloudinfra4:0727 .
                    docker push treeone008/ktcloudinfra4:0727
                '''
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    ansible master -m copy -a "src=deploy.yml dest=/root/deploy.yml"
                    ansible master -m shell -a "kubectl apply -f /root/deploy.yml --kubeconfig=/etc/kubernetes/admin.conf"
                '''
            }
        }
    }
}
