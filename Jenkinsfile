pipeline {
    agent { dockerfile true }
    stages {
        stage('Test') {
            steps {
                ant.replace(file: "index.html", token: "REPLACE_ME", value: "${BUILD_NUMBER}")
            }
        }
    }
}