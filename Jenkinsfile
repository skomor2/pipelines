pipeline{
    agent any 
    stages{
        stage("A"){
            steps{
                timestamps {
                    ansiColor('xterm') {
                        script {
                            properties([pipelineTriggers([pollSCM('H/2 * * * *')])])
                        }
                    git 'https://github.com/kamilszymanski/greeting-demo-app'
                    }
                chuckNorris()    
                }
            }
        }
        stage("B"){
            steps{
                 timestamps {
                     ansiColor('xterm') { 
                        sh './gradlew build'
                     }
                  jacoco exclusionPattern: '*Spec.class', execPattern: 'build/jacoco'
                  publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'build/reports/tests/test', reportFiles: '', reportName: 'HTML Report', reportTitles: ''])
                 }
                chuckNorris() 
            }
        }
        stage("C") { 
            steps {
                timestamps { 
                    ansiColor('xterm') { 
                        echo 'Testy Security'
                        sh 'sleep $((1 + RANDOM % 10))'
                    }
                }
                chuckNorris() 
            }
        }
        stage("D") { 
            steps {
                timestamps { 
                    ansiColor('xterm') { 
                        echo 'Production Deployment'

                    }
                input 'PODAJ LOGIN TWARDZIELU'
                }
                chuckNorris() 
            }
        }
    }


    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
