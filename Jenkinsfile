pipeline { // pipeline must be top level
    agent any // where to execute
    environment {
        // define env vars available for all stages in file
        NEW_VERSION = '1.3.0'
    }

    stages { // where the "work" happens
        stage("build") {

            steps {
                echo 'building the application...'
                echo "building version ${NEW_VERSION}"
            }
        }

        stage("test") {
            when {
                expression {
                    // define boolean expression here
                    BRANCH_NAME == 'dev'
                }
            }

            steps { // this steps will only execute if branch is dev
                echo 'testing the application...'
            }
        }

        stage("deploy") {

            steps {
                echo 'deploying the application...'
            }
        }
    }

    post {  // execute logic after all steps are done
        // conditions:
        always {

        }
        success {

        }
        failure {

        }

    }
}