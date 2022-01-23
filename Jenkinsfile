pipeline {
    agent any
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    environment {
        NEW_VERSION = '1.3.0'
    }
    tools {
        maven 'Maven'
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
                   params.executeTests == true
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
                    //sh 'echo $PASSWORD'
                    echo USERNAME
                    echo "THIS IS THE PASSWORD EVERYBODY -----------------> $PASSWORD"
                    echo "deploying version ${params.VERSION}"
                    echo "username is $USERNAME"
                }
            }
        }
    }
}