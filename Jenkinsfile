pipeline{
environment {
registry = "nayanavazhuthi/airbus"
registryCredential = '8e206c67-f527-42c9-86c1-3e62e32e9f67'
dockerImage = 'Dockerfile'
}
agent any
stages {
stage('SCM Checkout'){
steps{
git 'https://github.com/nayana212/Airbus.git'
}
}
stage('Mvn Package'){
steps{
sh "${mvnCMD} clean package"
}
}
stage('Building our image') {
steps{
script {
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage('Deploy our image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
}
}
