  pipeline {
   agent any

 stages {
   stage("Initial cleanup"){
     steps {
       dir("${WORKSPACE}"){
         deleteDir()
       }
     }
   }
   
    stage('Build') {
      steps {
        script {
         sh 'echo "Building Stage"'
       }
     }
   }

   stage('Test') {
     steps {
       script {
         sh 'echo "Testing Stage"'
       }
     }
   }
   stage('Package') {
     steps {
       script {
         sh 'echo "Packaging Stage"'
       }
     }
   }
   stage('Deploy') {
     steps {
       script {
         sh 'echo "Deploying Stage"'
       }
     }
   }
   
    stage('Checkout SCM') {
      steps {
            git branch: 'main', url: 'https://github.com/ssen280/Micorservices-website-helm-custom-chart.git'
      }
    }
    stage ('Package Artifact') {
    steps {
            sh 'zip -qr Micorservices-website-helm-custom-chart.zip ${WORKSPACE}/*'
     }

    }
    stage ('Upload Artifact to Artifactory') {
          steps {
            script { 
                 def server = Artifactory.server 'lke86053-131378-63b56d60ad4f'                 
                 def uploadSpec = """{
                    "files": [
                      {
                       "pattern": "online-shop-microservices-deployment-helm-file.zip",
                       "target": "saikat/online-shop-microservices-deployment-helm-file",
                       "props": "type=zip;status=ready"
                       }
                    ]
                 }""" 

                 server.upload spec: uploadSpec
               }
            }
  
        }

  
   }
 }
