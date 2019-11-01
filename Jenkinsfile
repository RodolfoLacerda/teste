pipeline {
    agent {
        docker { 
            image "qaninja/node-wd"
            args "--network=skynet"
        }
    }
    stages {
        stage('Build') {
            steps {
                sh "npm install"
                sh 'npm config ls'
            }
            
        }
        stage('Tests') {
            steps {
                sh "npm run test:ci"
            }
            post {
                always {
                    junit testDataPublishers:[[$class: 'AttachmentPublisher']], testResults: "tests_output/**/*.xml"
                }
            }
        }
    }
}