#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        jdk 'OpenJDK-15.0.2'
    }

    environment {
        VERSION = '0.0.2-SNAPSHOT'
    }

    stages {
        /*stage('Add Config files') {
            steps {
                configFileProvider([configFile(fileId: 'hello-spring-testing-gradle.properties', targetLocation: 'gradle.properties')]) {
                    sh './gradlew clean sonarqube'
                }
            }
        }*/

        /*stage('SonarQube analysis') {
            steps {
                withGradle {
                    sh './gradlew check'
                }
                withSonarQubeEnv(credentialsId: 'd79d7732-a255-4cad-8598-f577ea60755a', installationName: 'local') {
                    sh './gradlew sonarqube'
                }
            }
        }*/

        /*stage('Dependency Check') {
            steps {
                withGradle {
                    sh './gradlew dependencyCheckUpdate'
                    sh './gradlew dependencyCheckAnalyze'
                }
                dependencyCheck additionalArguments: ''' 
                    -o "./" 
                    -s "./"
                    -f "ALL" 
                    --prettyPrint''', odcInstallation: 'OWASP-DC'

                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }*/

        stage('Artifact') {
            steps {
                withCredentials([string(credentialsId: 'gitLabPrivateToken', variable: 'TOKEN')]) {
                    sh 'VERSION=${VERSION} ./gradlew publish'
                }
            }
        }
        
    }
}
