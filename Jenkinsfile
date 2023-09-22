pipeline {
    agent any
    stages { 
        stage('Clone') {
            steps {
                git branch: 'main', credentialsId: 'github-account', url: 'https://github.com/minhquoc1299/dc11-dot-quoctran-w4-terraform.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform') {
            steps {
                sh 'terraform fmt'
                sh 'terraform validate'
            }
        }

        stage('Terraform Plan Send Mail') {
            steps{
                script {
                        def planOutput = sh(script: 'terraform plan -out=tfplan', returnStdout: true).trim()
                        emailext subject: 'Terraform Plan for PR',
                                body: planOutput,
                                to: currentBuild.rawBuild.getCause(hudson.model.Cause$UserIdCause).getUserName(),
                                mimeType: 'text/plain'
                    }
            }
        }
       
    }

    // post { 
        
    //     success { 
    //         mail bcc: '', body: '${BUILD_NUMBER}-${BUILD_ID}-${BUILD_URL}-${NODE_NAME}-${JOB_NAME}', cc: 'manager@yopmail.com, tmquoc@tma.com.vn', from: '', replyTo: '', subject: '${BUILD_TAG}', to: ${CHANGES}
    //     }

    //     failure { 
    //         mail bcc: '', body: '${BUILD_NUMBER}-${BUILD_ID}-${BUILD_URL}-${NODE_NAME}-${JOB_NAME}', cc: 'manager@yopmail.com, tmquoc@tma.com.vn', from: '', replyTo: '', subject: '${BUILD_TAG}', to: ${CHANGES}
    //     }
    // }
}