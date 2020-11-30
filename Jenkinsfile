pipeline{
environment {
registry = "nayanavazhuthi/airbus"
registryCredential = '8e206c67-f527-42c9-86c1-3e62e32e9f67'
dockerImage = 'Dockerfile'
}
   stage('SCM Checkout'){
       git url: 'https://github.com/nayana212/Airbus.git'
   }
   stage('Mvn Package'){
     def mvnHome = tool name: 'maven-3', type: 'maven'
     def mvnCMD = "${mvnHome}/bin/mvn"
     sh "${mvnCMD} clean package"
   }
   stage('Build Docker Image'){
     sh 'docker build -t myhello:1.0'
   }
   stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
        sh "docker login -u kammana -p ${dockerHubPwd}"
     }
     sh 'docker push kammana/my-app:2.0.0'
   }
   }
