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
                sh 'mvn clean package'
                echo 'package completed successfully'
                sh 'ls' 
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying WAR file to remote Tomcat server'
                // sh 'sudo scp -i /var/jenkins_home/.ssh/practicekey.pem -o StrictHostKeyChecking=no target/javaCalculator.war centos@ec2-18-212-175-1.compute-1.amazonaws.com:/opt/tomcat/webapps/'
                sh '''
                    scp -i /var/jenkins_home/.ssh/practicekey.pem -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null target/javaCalculator.war centos@ec2-18-212-175-1.compute-1.amazonaws.com:/tmp/
                    ssh -i /var/jenkins_home/.ssh/practicekey.pem -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null centos@ec2-18-212-175-1.compute-1.amazonaws.com "sudo mv /tmp/javaCalculator.war /opt/tomcat/webapps/"
                    '''
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