pipeline {
  agent any

  tools {
    maven 'M2_HOME'
    }
  
  stages {
    stage('CheckOut') {
      steps {
        echo 'Checkout the source code from GitHub'
        git branch: 'main', url: 'https://github.com/Balunideepak/insuranceproject.git'
            }
    }
    
    stage('Package the Application') {
      steps {
        echo " Packaing the Application"
        sh 'mvn clean package'
            }
    }
        
    stage('Docker Image Creation') {
      steps {
        sh 'docker build -t balunideepak/insureprojectmar11:latest .'
            }
    }
    stage('DockerLogin') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'Docker-Hub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
}
            }
    }

    stage('Push Image to DockerHub') {
      steps {
        sh 'docker push balunideepak/insureprojectmar11:latest'
            }
    }
    stage('port expose'){
            steps{
                sh 'docker run -dt -p 8080:8081 --name c001 balunideepak/insureprojectmar11:latest'
            }
        }       
  }
}
