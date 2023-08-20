pipeline {
    agent any
    stages {
        stage("stage1") {
            steps {
                sh 'echo stage1'
            }
        }
        stage("Approval for stage2") {
            steps {
                script {
                    def userInput = input(
                        id: 'approvalForStage2',
                        message: 'Do you want to proceed with Stage 2?',
                        parameters: [
                            choice(
                                choices: ['Yes', 'No'],
                                description: 'Proceed with Stage 2?'
                            )
                        ]
                    )
                    if (userInput == 'Yes') {
                        echo "Approved to run Stage 2"
                    } else {
                        error "Skipped Stage 2 as per user's choice"
                    }
                }
            }
        }
        stage("stage2") {
            when {
                expression {
                    currentBuild.resultIsBetterOrEqualTo('SUCCESS')
                }
            }
            steps {
                sh 'echo stage2'
            }
        }
        stage("stage3") {
            steps {
                sh 'echo stage3'
            }
        }
    }
}
