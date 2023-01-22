pipeline {
    agent any
    stages {
         stage("test") {
             steps {
                 script { 
                    echo "test"
                  }
             }
        }
        stage("build npm") {
             steps {
                 script { 
                    echo "build the app"
                    sh 'npm run build'
                 }
             }
        }
        stage("build image") {
             steps {
                 script { 
                    echo "build the app"
                    withCredentials([usernamePassword(credentialsId:'Docker-hub-repo',passwordVariable:'PASS',usernameVariable: 'USER')]){
                    sh 'docker build -t akram6trimech9/demo-app:6.9'
                    sh "echo $PASS | docker login -u $USER  --password-stdin"
                    sh 'docker push akram6trimech9/demo-app:6.9'    
                  }
                 }
             }
        }
        stage("Deploy"){
             steps{
                 echo "deploying the app" 
                 }
        }
    }
}
