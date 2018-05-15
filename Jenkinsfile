@Library('jenkins-library') _

pipeline {
    agent none
    environment {
        NODE_VER = '8.1.0'
    }

    // put the post block at the beginning so that you guarantee it happens even if the script is failed partway through
    // post {
    //     success {

    //     }
    // }

    // // global options for build
    // //  ie how long to wait before timing out an approve
    // options {
    //     // if you don't have slaves, then you can skip the automatic/default checkout
    //     // jenkins assumes you have slaves and therefore checks out the code every time
    //     skipDefaultCheckout() 
    // }
    
    // what tools to install on the executor node to run this?
    // tools {
    //     // can do docker in here?
    // }



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
            when {
                anyOf {
                    branch 'Stage'
                }
            }
            steps {
                input 'Deploy to stage?'
            }
        }

        stage('parallel') { 
            // if any parallel stage task fails, then fail the whole thing immediately don't wait for the rest to finish
            failFast true

            parallel {
                stage('Build 1') {agent any
                    steps{
                         echo "blah"
                    }
                }

                stage("Build 2"){agent any
                    steps{
                         call()
                    }
                }
            }

        }
    }
}