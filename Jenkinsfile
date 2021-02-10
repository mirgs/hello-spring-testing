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

        /*stage('Artifact') {
            steps {
                archiveArtifacts 'build/libs/*.jar'
                withCredentials([string(credentialsId: 'gitLabPrivateToken', variable: 'TOKEN')]) {
                    sh './gradlew publish'
                }
            }
        }*/

        stage('Archiva') {
            steps {
                archiveArtifacts 'build/libs/*.jar'
                withCredentials([string(credentialsId: '7e9fde4f-7af2-4ce8-bb7f-937a2c9fdb08', aliasVariable : 'NAME', passwordVariable : 'PASS')]) {
                    sh './gradlew publish'
                }
            }
        }
        
    }
}
