pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                echo 'checking out branch'
                git branch: 'main', url: 'https://github.com/misschiomaa/javacalculator.git'
            }
        }
        stage('Build') {
            steps {
                // Build the Java project using Maven
                echo 'building my calculator'
                // sh 'pwd'
                // sh 'ls -la'
                sh 'mvn clean compile'
            }
        }
        // stage('Test') {
        //     steps {
        //         // Run unit tests
        //         sh 'mvn test'
        //         }
        //     post {
        //         always {
        //             // Publish JUnit test results
        //             junit '**/target/surefire-reports/*.xml'
        //         }
        //     }
        // }
        // stage('Package') {
        //     steps {
        //         // Package the application
        //         sh 'mvn package'
        //     }
        // }
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
            cleanWs()
        }
    }
}