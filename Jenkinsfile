pipeline {
agent any
stages {
    stage('Checkout') {
            steps {
                checkout scm
            }
        }
    stage('Init') {
        steps {
            bat './mvnw clean'
        }
    }

    stage('Test') {
        steps {
            bat './mvnw test'
            junit '**/target/surefire-reports/*.xml'
        }
    }
    stage('Build') {
        steps {
            bat './mvnw install'
            archiveArtifacts artifacts: 'target/*.jar'
        }
    }
stage('Documentation') {
    steps {
        bat './mvnw javadoc:javadoc'
        bat "xcopy /E /I /Y target\\site site"

        archiveArtifacts artifacts: 'target/site/**', fingerprint: true
    }
}

    stage('Deploy') {
        steps {
            echo 'Deploying...'
        }
    }


}
    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}