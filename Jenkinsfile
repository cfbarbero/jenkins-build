pipeline {
    agent none
    environment {
        NODE_VER = '8.1.0'
    }

    stages {
        stage('Beginning') { agent any
            environement{
                NODE_VER = '9.0'
            }
            steps {
                echo 'Hello World'
                sh 'echo $NODE_VER'
                echo "${env.NODE_VER}"
            }
        }

        stage('who am i?'){ agent any
            steps{
                sh 'host -t TXT pgp.michaelholley.us | awk -F \'"\' \'{print $2}\''
                sh 'echo $NODE_VER'
                
            }}
    }
}