pipeline {
    agent any
    triggers {
        GenericTrigger(
            genericVariables: [
                [key: 'pr_ref', value: '$.pull_request.head.ref', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],
                [key: 'sha', value: '$.pull_request.head.sha', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],
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
        stage('Pipeline 2: User commit and pull request'){
            steps{
                script {
                    // Make an HTTP GET request to the API
                    def response = httpRequest(
                        url: ${url_commit}.replaceAll("\\{\\/sha\\}", ${sha}),
                        acceptType: 'APPLICATION_JSON'
                    )

                    // Check if the request was successful (HTTP status code 200)
                    if (response.status == 200) {
                        def jsonResponse = readJSON text: response.content

                        // Now you can work with the JSON data
                        echo "Received JSON data: ${jsonResponse}"

                        // Example: Accessing a specific field in the JSON
                        def fieldValue = jsonResponse.fieldName
                        echo "Value of 'fieldName': ${fieldValue}"
                    } else {
                        error "API request failed with status ${response.status}"
                    }
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
