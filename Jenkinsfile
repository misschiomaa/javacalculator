pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                echo 'checking out branch'
                git branch: 'main', url: 'https://github.com/misschiomaa/javacalculator.git'
            }
        }
        stage('Build') {
            steps {
                echo 'building my calculator'
                sh 'mvn clean compile'
                echo 'build step completed'
            }
        }
        stage('Test') {
            steps {
                echo 'starting unit testing'
                sh 'mvn test'
                echo 'test completed successfully'
                }
            // post {
            //     always {
            //         junit '**/target/calculator-reports/*.xml'
            //         echo 'test report publish successfully to /target/calculator-reports/'
            //     }
            // }
        }
        stage('Package') {
            steps {
                // Package the application
                sh 'mvn package'
            }
        }
        // stage('Deploy') {
        //     steps {
        //         // Deploy the application (example for deploying to a server)
        //         // This step will vary based on your deployment target
        //         sh 'scp target/myapp.jar user@your-server-ip:/path/to/deploy'
        //     }
        // }
    }
    
    post {
        always {
            // Clean up workspace after build
            // cleanWs()
            echo 'cleaning up workspace'
        }
    }
}