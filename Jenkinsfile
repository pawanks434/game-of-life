pipeline {
    agent any
    triggers {cron ('H/15 * * * *')}
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
                sh 'mvn package'
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