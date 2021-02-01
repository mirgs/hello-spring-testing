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
        
        stage('pitest') {
            steps {
                withGradle {
                    sh './gradlew clean pitest'
                }
                step([$class: 'PitPublisher', 
                     mutationStatsFile: 'build/reports/pitest/**/mutations.xml', 
                     minimumKillRatio: 50.00, 
                     killRatioMustImprove: false
                ])
            }
        }        
        
    }
}
