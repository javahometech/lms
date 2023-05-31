@Library("jhc-libs") _

pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            when {
                branch "develop"
            }
            steps {
               git branch: 'main', credentialsId: 'javahometech', url: 'https://github.com/javahometech/lms'
            }
        }
        stage('Maven Build') {
            when {
                branch "develop"
            }
            steps {
               sh 'mvn clean package'
            }
        }
        
        stage('Dev Deploy') {
            when {
                branch "develop"
            }
            steps {
                tomcatDeploy("ec2-user","172.31.14.193","tomcat-dev","lms")
            }
        }
        stage('Stage Deploy') {
            when {
                branch "stage"
            }
            steps {
                tomcatDeploy("ec2-user","172.31.14.193","tomcat-dev","lms")
            }
        }
        stage('Prod Deploy') {
            when {
                branch "main"
            }
            steps {
                tomcatDeploy("ec2-user","172.31.14.193","tomcat-dev","lms")
            }
        }
        
    }
}
