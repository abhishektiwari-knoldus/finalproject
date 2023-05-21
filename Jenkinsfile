pipeline {
    agent any

    stages {
        stage('docker build.') {
            steps {
                sh 'docker build . -t abhishek00007/lto:v.${BUILD_NUMBER}'
               
            }
            
        }
        stage('docker login'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dochub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u abhishek00007 -p ${dockerhubpwd}'
                    
                            }
                      }
                 }
    }
        stage('docker image pushh')
        {
             when {
                branch "master"
                  }
            steps
            {
                 sh 'docker push abhishek00007/lto:v.${BUILD_NUMBER}'
            }
        }
        stage('deploy k8ss')
        {
             when {
                branch "master"
            }
            steps
            {
              withKubeConfig([credentialsId: '0fe6a189-a124-43d0-8fcf-d3f27ac0fa63']) {

              sh 'kubectl apply -f deploy.yml'  
              sh 'kubectl set image deployment/ltodeploy lto-container=abhishek00007/lto:v.${BUILD_NUMBER}'
              
              
}
               
            }
        }
    }
}
