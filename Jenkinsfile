pipeline {
    agent any
    stages {
        stage('Clean_workspace') {
            steps {
                deleteDir()
                sh 'ls -lah'
            }
        }
        stage('Clone_repository') {
            /* Let's make sure we have the repository cloned to our workspace */
            steps {
                checkout scm
            }
        }

        stage('Rename_build_in_index') {
            steps {
                def text = readFile file: "index.html"
                text.replaceAll("REPLACE_ME", "${BUILD_NUMBER}")
            }
        }

        stage('Build_image') {
            steps {
                docker.build("yonatanorr/blaze_meter")
            }
        }
    }
}
