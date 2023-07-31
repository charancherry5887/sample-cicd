pipeline {
    agent any
    tools {
        maven "maven3.9.3"
    }
    stages {
        stage ('Checkout code') {
            steps {
                git credentialsId: 'gitcred', url: 'https://github.com/Narendra969/sample-cicd.git'
            }
        }
        stage ('Build') {
            steps {
                sh "mvn clean package"
            }
        }
         stage ('Execute SonarQube Report') {
            steps {
                sh "mvn sonar:sonar"
            }
        }
         stage ('Deploy') {
            steps {
                sshagent(['tomcat']) {
                    sh 'scp -o StrictHostKeyChecking=no target/maven-web-application.war ubuntu@172.31.88.211:/home/ubuntu/tomcat/webapps'
                }
            }
        }
    }
}