#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        jdk 'OpenJDK-11.0.2'
    }

    stages {
        stage('Start') {
            steps {
                git url: 'hhttp://10.250.10.2:8929/root/hello-spring-testing.git', branch: 'master'
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
