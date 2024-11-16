pipeline {
    agent any

    stages {
        stage('Hello pull code from github') {
            steps {
               git 'https://github.com/sampathajith/k8s_project_nov24.git'
            }
        }


     stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t sampathk8simage /var/lib/jenkins/workspace/k8s_build_nov24'
                sh 'sudo docker tag sampathk8simage pardockerhub/sampathk8simage:latest'
                sh 'sudo docker tag sampathk8simage pardockerhub/sampathk8simage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push pardockerhub/sampathk8simage:latest'
                sh 'sudo docker image push pardockerhub/sampathk8simage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/k8s_build_nov24/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
}
}   
