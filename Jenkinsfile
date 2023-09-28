pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
  }
   stages {
   stage('Building image') {
      steps{
          sh ''' 
          docker build -t testapp .
             '''  
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }
   stage('Deploy Image') {
      steps{
        withCredentials([string(credentialsId: 'DockerHubPwd', variable: 'dockerpwd')]) {
          sh "docker login -u username -p ${dockerpwd}"
          sh '''
            docker tag testapp  127.0.0.1:8083/repository/docker/mguazzardo/testapp
            docker push  127.0.0.1:8083/repository/docker/mguazzardo/testapp   
          '''
          }
        }
      }
    }
}


    
  

