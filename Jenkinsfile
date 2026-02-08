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
            script {
                bat './mvnw javadoc:javadoc'

                bat 'if exist doc rmdir /S /Q doc'
                bat 'mkdir doc'

                bat 'xcopy /E /I /Y target\\site doc'

                bat 'powershell -Command "Compress-Archive -Path doc\\* -DestinationPath doc.zip"'

                archiveArtifacts artifacts: 'doc.zip', fingerprint: true
            }
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