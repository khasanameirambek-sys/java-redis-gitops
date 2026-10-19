pipeline {
agent any
environment {
IMAGE = "<dockerhub-username>/java-app"
TAG   = "${env.BUILD_NUMBER}"
}
stages {
stage('Checkout')      { steps { checkout scm } }
stage('Build Image')   { steps { sh 'docker build -t $IMAGE:$TAG .' }}
stage('Security Scan') { steps { sh 'trivy image --exit-code 1 --severity CRITICAL,HIGH $IMAGE:$TAG' } }
stage('Push Image')    { steps { sh 'docker push $IMAGE:$TAG' } }
}
}
