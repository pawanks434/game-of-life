pipeline {
    agent any
    triggers { pollSCM ('H/15 * * * *') }  
    parameters { string(name: 'MAVEN_GOA:', defaultValue: 'package', description: 'MVN_GOAL') }
    stages {
        stage ('vcs') {
            steps {
                git url: 'https://github.com/pawanks434/game-of-life.git',
                branch: 'declarative'
            } 
        }
        stage ('package') {
            tools {
                jdk 'JDK8_UBUNTU'
            }
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }
        stage ('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war'
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
   }
}