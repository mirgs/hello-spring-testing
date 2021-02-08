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

        /*stage('Test') {
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
        }*/
        
        //stage('pitest') {
        //    steps {
        //        withGradle {
        //            sh './gradlew clean pitest'
        //        }
        //        step([$class: 'PitPublisher', 
        //             mutationStatsFile: 'build/reports/pitest/**/mutations.xml', 
        //             minimumKillRatio: 50.00, 
        //             killRatioMustImprove: false
        //        ])
        //   }
        //} 

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
                    junit 'build/test-results/test/TEST-*.xml'
                    recordIssues(
                        enabledForFailure: true, aggregatingResults: true, 
                        tools: [java(), checkStyle(pattern: 'build/reports/checkstyle/*.xml', reportEncoding: 'UTF-8')]
                    )
                    publishHTML (target: [
                        reportDir: 'build/reports/pmd/',
                        reportFiles: '*.xml',
                        reportName: "Reporte PMD"
                    ])

                }
            }
        }      
        
    }
}
