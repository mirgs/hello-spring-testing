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
                    sh './gradlew assemble'
                }
            }
            post {
                success {
                    archiveArtifacts 'build/libs/*.jar'
                }
            }
        }

        stage('Test') {
            steps {
                withGradle {
                    sh './gradlew clean check'
                }
            }
            post {
                always {
                    recordIssues enabledForFailure: true, tool: spotBugs(pattern: 'build/reports/pmd/*.xml')

                }
            }
        }      
        
    }
}
