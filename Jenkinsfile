def gv 
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
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        
        stage("build") {
            steps {
                script {
                    gv.buildApp()
                }
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
                script {
                    gv.testApp()
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
                withCredentials([usernamePassword(credentialsId: 'server-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    //sh 'echo $PASSWORD'
                    echo USERNAME
                    echo "THIS IS THE PASSWORD EVERYBODY -----------------> $PASSWORD"
                    echo "username is $USERNAME"
                }
            }
        }
    }
}