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
        bat '''
        mkdir -p doc
        cp -r target/site/* doc/
        zip -r doc.zip doc
        '''
        archiveArtifacts artifacts: 'doc.zip'
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