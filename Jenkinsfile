pipeline {
    agent any

    stages {

        stage('CheckOut Code') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kathylm/sample-docker-react.git']])
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t clmkathy/sample-app:jks .'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Put your testing command here if you have'
            }
        }
        stage('Publish Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub_kathy', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                    sh '''
                        docker login -u $USERNAME -p $PASSWORD
                        docker image push clmkathy/sample-app:jks
                    '''
                }
            }
        }        
        
    }
}
