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
                echo 'package completed successfully'
                sh 'ls target/' 
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying WAR file to remote Tomcat server'
                sh 'scp -i /var/jenkins_home/.ssh/practicekey.pem -o StrictHostKeyChecking=no target/RaviCalculator-1.4.jar centos@ec2-18-212-175-1.compute-1.amazonaws.com:/opt/tomcat/webapps/'
                echo 'deployed calculator successfully'
            }
        }
    }
    
    post {
        always {
            // Clean up workspace after build
            // cleanWs()
            echo 'cleaning up workspace'
        }
    }
}