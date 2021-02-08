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
                    //sh './gradlew test'
                    //sh './gradlew pmdTest'
                    sh './gradlew clean check'
                }
            }
            post {
                always {
                    recordIssues enabledForFailure: true, tool: pmdParser(pattern: 'build/reports/pmd/*.xml')

                    //publishHTML (target: [
                    //    reportDir: 'build/reports/pmd/',
                    //    reportFiles: '*.html',
                    //    reportName: "Reporte PMD"
                    //])

                }
            }
        }      
        
    }
}
