pipeline {
agent any
stages {
    stage('Build') {
        steps {
            bat './mvnw clean install'
            archiveArtifacts artifacts: 'target/*.jar'
        }
    }
    stage('Test') {
        steps {
            junit '**/target/surefire-reports/*.xml'
        }
    }
    stage('Deploy') {
        steps {
            echo 'Deploying...'
        }
    }
}}