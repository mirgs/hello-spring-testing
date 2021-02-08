#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        jdk 'OpenJDK-15.0.2'
    }

    stages {
        /*stage('Add Config files') {
            steps {
                configFileProvider([configFile(fileId: 'hello-spring-testing-gradle.properties', targetLocation: 'gradle.properties')]) {
                    sh './gradlew clean sonarqube'
                }
            }
        }*/

        stage('SonarQube analysis') {
            steps {
                withGradle {
                    sh './gradlew check'
                }
                withSonarQubeEnv(credentialsId: 'd79d7732-a255-4cad-8598-f577ea60755a', installationName: 'local') {
                    sh './gradlew sonarqube'
                }
            }
        }
        
    }
}
