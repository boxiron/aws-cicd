pipeline {
    agent any 

    stages {
        stage('git checout'){
            steps{
                git branch: 'main', url: 'https://github.com/boxiron/aws-cicd.git'
            }
        }
        stage('test'){
            steps{
                sh 'echo test'
            }
        }
        stage('god is good'){
            steps{
                sh 'echo god is good'
            }
        }
    }
}