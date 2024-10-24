pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
          
                    sh 'mvn clean package' 
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'mvn test' // Run your tests
                }
            }
        }
        stage('Deploy') {
            when {
                branch 'main' // Deploy only on the main branch
            }
            steps {
                script {
                    // Add your deployment commands here
                    echo 'Deploying application...'
                    // e.g., sh './deploy.sh'
                }
            }
        }
    }

    post {
        always {
            // Archive test results, etc.
            junit '**/target/surefire-reports/*.xml' // Adjust this if your reports are in a different location
            // Clean up workspace if necessary
            cleanWs()
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
