pipeline{
    agent any
    options {
        timestamps() 
    }
    stages{
        stage("A"){
            steps{

                    ansiColor('xterm') {
                        script {
                            properties([pipelineTriggers([pollSCM('H/2 * * * *')])])
                        }
                    git 'https://github.com/kamilszymanski/greeting-demo-app'
                    }
 
                
            }
        }
        stage("B"){
            steps{

                     ansiColor('xterm') { 
                        sh './gradlew build'
                     }
                  jacoco exclusionPattern: '*Spec.class', execPattern: 'build/jacoco'
                  publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'build/reports/tests/test', reportFiles: '', reportName: 'HTML Report', reportTitles: ''])
                 

            }
        }
        stage("C") { 
            steps {
 
                    ansiColor('xterm') { 
                        echo 'Testy Security'
                        sh 'sleep $((1 + RANDOM % 10))'
                    }
                

            }
        }
        stage("D") { 
            steps {

                    ansiColor('xterm') { 
                        echo 'Production Deployment'

                    }
                input 'PODAJ LOGIN TWARDZIELU'
                

            }
        }
    }


    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
            chuckNorris()
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
