pipeline {
    agent none
    environment {
        NODE_VER = '8.1.0'
    }

    stages {
        stage('Beginning') { agent any
            environment{
                DEPLOY_VERSION = 'stage'
            }
            steps {
                echo 'Hello World'
                sh 'echo $NODE_VER'
                echo "${env.DEPLOY_VERSION}"
            }
        }

        stage('who am i?'){ agent any
            steps{
                sh 'host -t TXT pgp.michaelholley.us | awk -F \'"\' \'{print $2}\''
                sh 'echo $NODE_VER'
                
            }
        }

        // Use agent none when asking for user input so that you don't tie up an executor waiting
        stage('Deploy to stage?') { agent none
            step {
                input 'Deploy to stage?'
            }
        }
    }
}