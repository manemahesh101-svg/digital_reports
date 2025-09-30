pipeline {
    agent any

    tools {
        maven 'Maven'   // Configure Maven in Jenkins (Manage Jenkins → Global Tool Configuration)
        jdk 'JDK11'     // Configure Java in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Pulling code from Git repository..."
                git branch: 'main', url: 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building the project..."
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                echo "Packaging the artifact..."
                sh 'mvn package'
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application to Tomcat server..."
                sh 'cp target/*.war /opt/tomcat/webapps/'  // Adjust Tomcat path as per your setup
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed. Please check logs."
        }
    }
}
