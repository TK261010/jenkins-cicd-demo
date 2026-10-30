
pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'if not exist build mkdir build'
                bat 'copy /Y index.html build\\index.html'
            }
        }

        stage('Test') {
            steps {
                bat 'if exist build\\index.html (echo TEST PASSED) else (echo TEST FAILED & exit /b 1)'
            }
        }

        stage('Deploy') {
            steps {
                bat 'if not exist deploy mkdir deploy'
                bat 'copy /Y build\\index.html deploy\\index.html'
            }
        }
    }

    post {
        success {
            echo 'CI/CD completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
