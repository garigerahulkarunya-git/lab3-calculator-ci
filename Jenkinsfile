pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package JAR') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Create DEB') {
            steps {
                sh '''
                fpm -s dir -t deb \
                -n calculator-app \
                -v 1.0 \
                target/calculator-app-1.0-SNAPSHOT.jar=/usr/local/bin/calculator.jar
                '''
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: '*.deb', fingerprint: true
            }
        }
    }
}
