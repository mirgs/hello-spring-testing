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
            post {
                success {
                    archiveArtifacts 'build/libs/*.jar'
                }
            }
        }
        stage('Test') {
            steps {
                withGradle {
                    sh './gradlew test'
                    sh './gradlew test jacocoTestReport'
                }
            }
            post {
                always {
                    junit 'build/test-results/test/TEST-*.xml'
                }
            }
        }
        stage('Build-jacoco') {
            steps {
                jacocoCodeCoverage { 
                    execPattern('build/jacoco/*.exec')
                    classPattern('build/classes')
                    sourcePattern('src/main/java')
                    exclusionPattern('src/test*)
                }
            }
        }
        
    }
}
