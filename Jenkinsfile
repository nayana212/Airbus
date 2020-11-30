pipeline {
environment {
registry = "nayanavazhuthi/airbus"
registryCredential = '8e206c67-f527-42c9-86c1-3e62e32e9f67'
dockerImage = 'Dockerfile'
}
agent any
stages {
stage('Clone code from Git') {
steps {
git 'https://github.com/nayana212/Airbus.git'
}
}
stage('Build Docker image') {
steps{
script {
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage('Maven'){
sh "mvn clean install"}
}
stage('Deploy image to Dockerhub') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
}


