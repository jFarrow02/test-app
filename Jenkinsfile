pipeline { // pipeline must be top level
    agent any // where to execute
    parameters {
        string(name: 'VERSION', defaultValue: '', description: '')
        // choice(name: 'VERSION', choices: ['1.1', '1.2', '1.3'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    // tools { // access gradle, maven, and JDK only
    //     maven ''

    // }
    environment {
        // define env vars available for all stages in file
        NEW_VERSION = '1.3.0'
        NEXUS_CREDENTIALS = credentials('nexus-creds') // credentials('{credentialId}')
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
                    // env.BRANCH_NAME == 'dev'
                    params.executeTests == true
                }
            }

            steps { // this steps will only execute if branch is dev
                echo 'testing the application...'
            }
        }

        stage("deploy") {

            steps {
                echo 'deploying the application...'
                // use withCredentials when you need creds in a single stage
                withCredentials([
                    usernamePassword(credentials: 'nexus-credentials', usernameVariable: USER,
                    passwordVariable: PWD)
                ]) {
                    echo "Username: ${USER}"
                }
            }
        }
    }

    post {  // execute logic after all steps are done
        // conditions:
        always {
            echo 'pipeline finished'
        }
        success {
            echo 'pipeline succeeded'
        }
        failure {
            echo 'pipeline failed'
        }

    }
}