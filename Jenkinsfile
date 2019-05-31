pipeline {
    agent { label 'master' }
    stages {
        stage('checkout') {
            
            
            steps {
               println("Checkout existing JARS from interview-test repo. ") 
               dir('interview-test'){
                   git branch: 'master',
                   url: 'https://git@github.com/SlashTec/interview-test.git'
        
               }
                 
                   
                                   script  {
                   sha1sum = sh(returnStdout: true, script: "sha1sum interview-test/airports-assembly-1.0.1.jar")
                   print sha1sum
                   if (sha1sum.contains("0bd35ea555b9aabaf30d255f3cb90aedf6bebca1")){
                     println("sha1 check passed")
                    } else {
                      println("sha2 check failed")
                      error "This pipeline stops here!"
                }
                   }
                   //sha1 "airports-assembly-1.0.1.jar"
                
                sh "ls -rtlh"   
                //sh 'minikube start'
            }
        }
    }
}
