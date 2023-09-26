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
        )
    }
    stages {
        stage('Pipeline 1: Pull Request Validation') {
            steps {
                script {
                    echo "Pipeline Pull Request Validation"
                    echo "ref ${ref}"
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
