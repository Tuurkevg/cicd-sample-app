pipeline {
    agent any
    triggers {
        pollSCM('H/2 * * * *')  // Controleer elke 2 seconden op nieuwe commits
    }
    stages {
        stage('Preparation') {
            steps {
                catchError(buildResult: 'SUCCESS') {
                    sh 'docker stop samplerunning || true'
                    sh 'docker rm samplerunning || true'
                }
            }
        }
        stage('Build') {
            steps {
                build job: 'BuildSampleApp'  // Bouw je app (kan aangepast worden naar je eigen build-stap)
            }
        }
        stage('Results') {
            steps {
                build job: 'TestSampleApp'  // Voer de testjob uit
            }
        }
    }
}
