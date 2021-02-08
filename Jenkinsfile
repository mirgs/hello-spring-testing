#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        jdk 'OpenJDK-15.0.2'
    }

    stages {
        stage('Add Config files') {
            steps {
                configFileProvider([configFile(fileId: 'hello-spring-testing-gradle.properties', targetLocation: 'gradle.properties')]) {
                    sh './gradlew iT'
                }
            }
        }
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
                    sh './gradlew clean sonarqube'
                }
            }
            post {
                always {
                    recordIssues enabledForFailure: true, tool: sonarQube(pattern: 'build/sonar/*.xml')

                }
            }
        }      
        
    }
}
