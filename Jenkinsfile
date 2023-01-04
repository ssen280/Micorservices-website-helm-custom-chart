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
    stage('Upload Artifact to Artifactory') {
      steps {
        script { 
                def server = Artifactory.server 'artifactory'                 
                def uploadSpec = """{
                    "files": [
                      {
                       "pattern": "php-todo.zip",
                       "target": "artifacts-todo-php",
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
