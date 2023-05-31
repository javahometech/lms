@Library("jhc-libs") _

pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
               git branch: 'main', credentialsId: 'javahometech', url: 'https://github.com/javahometech/lms'
            }
        }
        stage('Maven Build') {
            steps {
               sh 'mvn clean package'
            }
        }
        
        stage('Dev Deploy') {
            steps {
                tomcatDeploy("ec2-user","172.31.14.193","tomcat-dev","lms")
            }
        }
        
    }
}
