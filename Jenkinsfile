pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials("aws-secret-key-id-env-main")
        AWS_SECRET_ACCESS_KEY = credentials("aws_secret_access_key_env_main")
    }
    stages { 
        stage('Clone') {
            steps {
                git branch: 'main', credentialsId: 'github-account', url: 'https://github.com/minhquoc1299/dc11-dot-quoctran-w4-terraform.git'
            }
        }

        stage('Terraform Init') {
            steps {
                script {
                    sh 'terraform init'
                    echo '[Debug] Running terraform init successfully~'
                    def workspaceList = sh(script: 'terraform workspace list', returnStatus: true)
                    if (workspaceList.contains(env.BRANCH_NAME)){
                        echo 'Workspace ${env.BRANCH_NAME} already exists'
                    }else {
                        sh 'terraform workspace new ${env.BRANCH_NAME}'
                        echo 'Workspace ${env.BRANCH_NAME} created'
                    }    
                 
                    sh 'terraform workspace select ${env.BRANCH_NAME}'
                    echo '[Debug] Running terraform workspace select successfully~'
                }
            }
        }

        stage('Terraform Validate') {
            steps {
                sh 'terraform fmt'
                sh 'terraform validate'
            }
        }
       
    }

    post { 
        
        success { 
            mail bcc: '', body: '${BUILD_NUMBER}-${BUILD_ID}-${BUILD_URL}-${NODE_NAME}-${JOB_NAME}', cc: 'manager@yopmail.com, tmquoc@tma.com.vn', from: '', replyTo: '', subject: '${BUILD_TAG}', to: env.CHANGES
        }

        failure { 
            mail bcc: '', body: '${BUILD_NUMBER}-${BUILD_ID}-${BUILD_URL}-${NODE_NAME}-${JOB_NAME}', cc: 'manager@yopmail.com, tmquoc@tma.com.vn', from: '', replyTo: '', subject: '${BUILD_TAG}', to: env.CHANGES
        }
    }
}