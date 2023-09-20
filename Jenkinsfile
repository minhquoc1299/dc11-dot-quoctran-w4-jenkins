pipeline {
    agent any
    stages { 
        stage('Clone') {
            steps {
                git branch: 'main', credentialsId: 'github-account', url: 'https://github.com/minhquoc1299/dc11-dot-quoctran-w4-terraform.git'
            }
        }

        stage('Init Provider') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Validate ') {
            steps {
                sh 'terraform fmt'
                sh 'terraform validate'
            }
        }
       
    }

    post { 
        always { 
            mail bcc: '', body: '''$BUILD_NUMBER
            $BUILD_ID
            $BUILD_URL
            $NODE_NAME
            $JOB_NAME''', cc: 'manager@yopmail.com', from: '', replyTo: '', subject: '$BUILD_TAG', to: 'tmquoc@tma.com.vn'
        }
    }
}