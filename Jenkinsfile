pipeline {
    agent any
    stages {
        stage('Clone repository') {
            /* Let's make sure we have the repository cloned to our workspace */
            checkout scm
        }

        stage('Rename build in index') {
            sh 'sed -i 's~REPLACE_ME~'${BUILD_NUMBER}'~' index.html'
        }

        stage('Build image') {
            docker.build("yonatanorr/blaze_meter")
        }
    }
}