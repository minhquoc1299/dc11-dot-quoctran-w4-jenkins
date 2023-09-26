pipeline {
    agent any
    triggers {
        GenericTrigger(
            genericVariables: [
                [key: 'pr_ref', value: '$.pull_request.head.ref', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],
                [key: 'pr_sha', value: '$.pull_request.head.sha', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],
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
    }
    stages {
        stage('Pipeline 1: Pull Request Validation') {
            steps {
                script {
                    echo "Pipeline Pull Request Validation"
                    echo "pr_ref ${pr_ref}"
                    echo "pr_sha ${pr_sha}"
                    echo "url_commit ${url_commit}"
                }
            }
        }

        stage('Pipeline 2: Apply Changes') {
           
            steps {
                script {
                    echo "Pipeline 2: Apply Changes"
                }
            }
        }
    }
}
