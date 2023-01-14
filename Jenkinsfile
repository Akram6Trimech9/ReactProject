pipeline {
    agent none
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dh_cred')
    }
    stages {
         stage('Checkout'){
            agent any
            steps{
                //Changez avec votre lien gitlab
                git branch: 'main', url: 'Put your git there '
            }
        }
        stage('Init'){
            agent any
            steps{
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin' //put your credentials here 
            }
        }
        stage('Build backend') {
            agent any
            when {
                changeset "**/*.**"
                beforeAgent true
            }
            steps {
                dir('backend'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/backend:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/backend:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/backend:$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }
        stage('Build frontend') {
            agent any
            when {
                changeset "**/client/*.*"
                beforeAgent true
            }
            steps {
                dir('client'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/frontend:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/frontend:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/frontend$BUILD_ID'
                    sh 'docker logout'
                }
            }
        }

    
    }
}

