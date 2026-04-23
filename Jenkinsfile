pipeline {
    agent any
    tools {
        maven 'Maven3' 
    }
    stages {
        stage('CHECKOUT') {
            steps {
                git 'https://github.com/vvce23ise0250-cmyk/c1_ayyo.git'
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean install'
                
            }
        }
        stage('Test') {
            steps {
            
                bat 'mvn test'
            
            }
        }
    }
    
    // ADD THIS SECTION FOR NOTIFICATIONS
    post {
        success {
            slackSend channel: '#general', 
                      color: 'good', 
                      message: "SUCCESS: Job '${env.JOB_NAME}' [${env.BUILD_NUMBER}] (${env.BUILD_URL})"
        }
        failure {
            slackSend channel: '#general', 
                      color: 'danger', 
                      message: "FAILURE: Job '${env.JOB_NAME}' [${env.BUILD_NUMBER}] (${env.BUILD_URL})"
            
            emailext body: "Build Failed! Check console output at: ${env.BUILD_URL}",
                     subject: "Build Failed: ${env.JOB_NAME}",
                     to: "vvce23ise0250@vvce.ac.in"
        }
    }
}