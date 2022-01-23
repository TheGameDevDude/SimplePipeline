pipeline {
    agent any
    environment {
        NEW_VERSION = '1.3.0'
    }
    stages {
        stage("build") {
            steps {
                echo 'building the application'
                echo "building version ${NEW_VERSION}"
            }
        }

        stage("test") {
            when {
                expression {
                    BRANCH_NAME == 'dev'
                }
            }
            steps {
                echo 'testing the application'
            }
        }

        stage("deploy") {
            steps {
                echo 'deploying the application'
                withCredentials([usernamePassword(credentialsId: 'server-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    // available as an env variable, but will be masked if you try to print it out any which way
                    // note: single quotes prevent Groovy interpolation; expansion is by Bourne Shell, which is what you want
                    //sh 'echo $PASSWORD'
                    // also available as a Groovy variable
                    echo USERNAME
                    // or inside double quotes for string interpolation
                    echo "username is $USERNAME"
                }
            }
        }
    }
}