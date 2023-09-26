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
        printContributedVariables: true,
        printPostContent: true
        )
    }
    stages {
        stage('Pipeline 1: Pull Request Validation') {
            steps {
                script {
                    echo "Pipeline 1: Pull Request Validation"
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
