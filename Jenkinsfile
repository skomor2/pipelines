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
                  publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'build/reports/test/test', reportFiles: '', reportName: 'HTML Report', reportTitles: ''])
                 }
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
