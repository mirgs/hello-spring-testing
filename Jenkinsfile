#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        jdk 'OpenJDK-15.0.2'
    }

    stages {
        stage('Build') {
            steps {
                withGradle {
                    sh './gradlew pitest'
                }
            }
            post {
                success {
                    bat 'mvn --batch-mode org.pitest:pitest-maven:mutationCoverage'
                }
            }
        }        
        
    }
}
