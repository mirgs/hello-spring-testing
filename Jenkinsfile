#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        jdk 'OpenJDK-15.0.2'
    }

    stages {
        stage('Start') {
            steps {
                git url: 'https://github.com/mirgs/hello-spring-testing.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                withGradle {
                    sh './gradlew assemble'
                }
            }
        }
        stage('Test') {
            steps {
                withGradle {
                    sh './gradlew test'
                }
            }
        }
        
    }
}
