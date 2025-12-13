pipeline {
    agent any

    environment {
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64"
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull code from GitHub
                git branch: 'main', url: 'https://github.com/Firasama29/spring-boot-docker-redis'
            }
        }

        stage('Build') {
            steps {
                // Use Maven to compile and package
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh './mvnw test'
            }
        }

        stage('Archive Artifact') {
            steps {
                // Save the built jar as artifact
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Build and tests passed ✅"
        }
        failure {
            echo "Build failed ❌"
        }
    }
}
