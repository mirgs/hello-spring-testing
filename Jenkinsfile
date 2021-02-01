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
                step([$class: 'PitPublisher', 
                     mutationStatsFile: 'build/reports/pitest/mutations.xml', 
                     minimumKillRatio: 50.00, 
                     killRatioMustImprove: false
                ])
            }
        }        
        
    }
}
