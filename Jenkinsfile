pipeline {
    agent any
    triggers { pollSCM ('H/15 * * * *') }  
    parameters { choice(name: 'MAVEN_GOAL', choices: ['package', 'clean', 'compile', 'install', 'clean package', 'clean test'], description: 'MVN-GL') }
    stages {
        stage ('vcs') {
            steps {
                git url: 'https://github.com/pawanks434/game-of-life.git',
                branch: 'declarative'
            } 
        }
        stage ('package') {
            steps {
                sh 'export PATH="/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH" && "mvn ${params.MAVEN_GOAL}"'
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