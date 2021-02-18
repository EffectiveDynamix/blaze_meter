pipeline {
    agent any
    stages {
        stage('Clean workspace') {
            deleteDir()
            sh 'ls -lah'
        }
        stage('Clone repository') {
            /* Let's make sure we have the repository cloned to our workspace */
            checkout scm
        }

        stage('Rename build in index') {
            def text = readFile file: "index.html"
            text.replaceAll("REPLACE_ME", "${BUILD_NUMBER}")
        }

        stage('Build image') {
            docker.build("yonatanorr/blaze_meter")
        }
    }
}
