pipeline {
    agent any
    triggers {
        GenericTrigger(
        genericVariables: [
            [key: 'ref', value: '$.ref']
        ],
        causeString: 'Triggered on $ref',
        regexpFilterExpression: '',
        regexpFilterText: '',
        token: 'RO3bV0fpMs',
        printContributedVariables: true,
        printPostContent: true,
        genericRequestVariables: [
            [key: 'requestWithNumber', regexpFilter: '[^0-9]'],
            [key: 'requestWithString', regexpFilter: '']
        ],
        genericHeaderVariables: [
            [key: 'headerWithNumber', regexpFilter: '[^0-9]'],
            [key: 'headerWithString', regexpFilter: '']
        ],
        )
    }
    stages {
        stage('Pipeline 1: Pull Request Validation') {
            steps {
                script {
                    echo "Pipeline Pull Request Validation"
                    echo "ref ${ref}"
                    echo "requestWithNumber ${requestWithNumber}"
                    echo "requestWithString ${requestWithString}"
                    echo "headerWithNumber ${headerWithNumber}"
                    echo "headerWithString ${headerWithString}"
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
