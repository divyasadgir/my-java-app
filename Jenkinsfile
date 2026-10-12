pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Check Java') {
            steps {
                bat 'java -version'
            }
        }

        stage('Build') {
            steps {
                bat '"C:/Maven/apache-maven-3.10.0/bin/mvn.cmd" clean compile'
            }
        }

        stage('Unit Test') {
            steps {
                bat '"C:/Maven/apache-maven-3.10.0/bin/mvn.cmd" test'
            }
            post {
                always {
                    junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                bat '"C:/Maven/apache-maven-3.10.0/bin/mvn.cmd" package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Application packaged successfully!'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
