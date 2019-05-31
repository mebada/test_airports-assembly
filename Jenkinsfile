pipeline {
    agent { label 'master' }
    stages {
        stage('Download JAR') {
           steps {
               println("Checkout existing JARS from interview-test repo. ") 
               dir('interview-test'){
                   git branch: 'master',
                   url: 'https://git@github.com/SlashTec/interview-test.git
               } 
               script {
                   def fileName = "airports-assembly-1.0.1.jar"
                   def expectedSHA1 = "0bd35ea555b9aabaf30d255f3cb90aedf6bebca1"
                   sh "echo ${fileName}" 
                   sha1sum = sh(returnStdout: true, script: "sha1sum interview-test/${fileName}")
                   print sha1sum
                   if (sha1sum.contains("${expectedSHA1}")){
                     println("sha1 check passed")
                    } else {
                      println("sha2 check failed")
                      error "This pipeline stops here!"
                   }
               } //end of script
                 
           } //end of steps
        } // end of stage  
        
        stage('Build Docker Image') {
            steps {
               script{
                     sh "eval \$(minikube docker-env)"
                     sh "docker build -t test_airports-assembly:v1  -f docker/Dockerfile . "
                     sh "kubectl cluster-info"
                     sh "helm init"
               }
            
            }
        } 
    } //end of stages
} // end of pipeline
