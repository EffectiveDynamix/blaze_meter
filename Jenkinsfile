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
                sh "sed -i 's~REPLACE_ME~'${BUILD_NUMBER}'~' index.html"
            }
        }

        stage('Build_image') {
            steps {
                script {
                    docker.build("blaze_meter")
                }
            }
        }
        stage('Kube_Deploy') {
            steps {
                script {
                    sh 'kubectl apply -f deployment.yaml'
                }
                script {
                    sh 'kubectl apply -f nginx_srv.yaml'
                }
            }
        }
    }
}
