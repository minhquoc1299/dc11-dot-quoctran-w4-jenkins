pipeline {
    agent any
    triggers {
        GenericTrigger(
            genericVariables: [
                [key: 'pr_ref', value: '$.pull_request.head.ref', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],
                [key: 'target_ref', value: '$.pull_request.base.ref', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],
                [key: 'pr_sha', value: '$.pull_request.head.sha', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],
                [key: 'pr_url', value: '$.pull_request.url', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],
                [key: 'url_commit', value: '$.repository.commits_url', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],

            ],
            causeString: 'Triggered on $ref',
            regexpFilterExpression: '',
            regexpFilterText: '',
            token: 'RO3bV0fpMs',
            printContributedVariables: true,
            printPostContent: true,
        )
    }
    environment {
        pr_user_email = ''
        pr_user_full_name = ''
    }
    stages {
        stage('Pipeline 1: Pull Request Validation') {
            steps {
                script {
                    echo 'Pipeline Pull Request Validation'
                    echo "pr_ref ${pr_ref}"
                    echo "pr_sha ${pr_sha}"
                    echo "url_commit ${url_commit}"
                }
            }
        }
        stage('Pipeline 2: User commit and pull request') {
            steps {
                script {
                    // https://api.github.com/repos/minhquoc1299/dc11-dot-quoctran-w4-terraform/commits{/sha}
                    def response = httpRequest(
                        url: url_commit.replaceAll("\\{\\/sha\\}", "/${pr_sha}"),
                        httpMode: 'GET',
                        acceptType: 'APPLICATION_JSON'
                    )

                    // Check if the request was successful (HTTP status code 200)
                    if (response.status == 200) {
                        def jsonResponse = readJSON text: response.content
                        pr_user_email = jsonResponse.commit.committer.email
                        pr_user_full_name = jsonResponse.commit.committer.name
                    } else {
                        error "API committer request failed with status ${response.status}"
                    }
                }
            }
        }

        stage('Pipeline 3: GIT Checkout SCM') {
            steps {
                checkout([$class: 'GitSCM',
                  branches: [[name: pr_ref]],
                  userRemoteConfigs: [[url: 'https://github.com/minhquoc1299/dc11-dot-quoctran-w4-terraform.git',
                                      credentialsId: 'github-account']]])
            }
        }

        stage('Pipeline 4: Terraform Validate') {
            steps {
                script {
                    sh 'terraform init'
                    sh 'terraform fmt'
                    sh 'terraform validate'
                }
            }
        }

        stage('Pipeline 4: Terraform Plan') {
            steps {
                script {
                    sh 'terraform plan -no-color > output.txt'
                }
            }
        }
    }

    post {
        failure {
            mail bcc: '', body: '''Dear ${pr_user_full_name},

            Terraform plan failed. Please check the build logs for details.
            Pull request: ${pr_url}

            Thanks,
            Jenkins System''', 
            cc: 'tmquoc@tma.com.vn', from: '', replyTo: '', subject: '[PR] Terraform PR Build Fail', to: pr_user_email
        }

        success {
        }
    }
}
