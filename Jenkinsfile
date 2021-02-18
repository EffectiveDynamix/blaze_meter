pipeline {
    environment {
        registry = "yonatanor/blaze"
        registryCredential = 'dockerHub'
        customImage = ''
    }
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
                    customImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('upload image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        customImage.push()
                        customImage.push('latest')
                    }
                }
            }
        }
        stage('Kube_Clean') {
            steps {
                script {
                    sh 'kubectl delete deployments nginx-deployment'
                }
            }
        }
        stage('Kube_Deploy') {
            steps {
                script {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}
