pipeline {
    agent any
    stages { 
        stage('Clone') {
            steps{
                echo 'Clone pipeline'
            }
        }
        stage('Build') {
            sh 'Build pipeline'
        }
        stage('Test') {
           sh 'Test pipeline'
        }
        stage('Deploy') {
            sh 'Deploy pipeline'
        }
    }
}
