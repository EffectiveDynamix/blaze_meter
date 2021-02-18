pipeline {
    agent any
    stages {
        stage('Clean_workspace') {
            deleteDir()
            sh 'ls -lah'
        }
        stage('Clone_repository') {
            /* Let's make sure we have the repository cloned to our workspace */
            checkout scm
        }

        stage('Rename_build_in_index') {
            def text = readFile file: "index.html"
            text.replaceAll("REPLACE_ME", "${BUILD_NUMBER}")
        }

        stage('Build_image') {
            docker.build("yonatanorr/blaze_meter")
        }
    }
}
