pipeline {
    agent any
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
        stage ('copy build') {
            steps {
            sh  'FOLDER="/tmp/${JOB_NAME}/${BUILD_ID}" && \
                 mkdir -p "${FOLDER}" && \
                 cp "./gameoflife-web/target/gameoflife.war" ${FOLDER}'
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