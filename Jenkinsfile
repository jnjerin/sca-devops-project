pipeline {
  agent any
    
  tools {nodejs "node"}
    
  stages {
        
    stage('Git') {
      steps {
        git 'https://github.com/****/****'
      }
       }  
    
            
    stage('Test') {
      steps {
        sh 'node test'
        script {
                    echo "testing app"
                }
      }
    }
     
    stage('Build app') {
      steps {
        sh 'npm install'
         sh '<<Build Command>>'
           script {
                    echo "building app"
                }
      }
       stage("build image") {
            steps {
                script {
                    echo "building image"
                }
    }  
      stage('Deploy') {
      steps {
                script {
                    echo "deploying"
      }
   
    }
  }
}

