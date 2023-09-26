pipeline {
    agent any
    triggers {
        GenericTrigger(
            genericVariables: [
                [key: 'ref', value: '$.ref', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],
                [key: 'ssh_url', value: '$.repository.ssh_url', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],
                [key: 'email_user_commit', value: '$.commits[*].committer.email', expressionType: 'JSONPath', regexpFilter: '', defaultValue: ''],
                [key: 'full_name_user_commit', value: '$.commits[*].committer.name', expressionType: 'JSONPath', regexpFilter: '', defaultValue: '']
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
                    echo "ssh_url ${ssh_url}"
                    echo "email_user_commit ${email_user_commit}"
                    echo "full_name_user_commit ${full_name_user_commit}"
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
