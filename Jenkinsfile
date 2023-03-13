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
                sh 'mvn testing'
            }
        }
        stage ('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war'
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
   }
   post {
     success {
        mail subject: "Jenkins build of ${JOB_NAME} with biuld id ${BUILD_ID} is success",
             body: "for more info refer the build URL ${BUILD_URL}",
             from: 'pawanks434@gmail.com',
             to: 'team-all-qt@qt.com'   
     }
      failure {
            mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is failed",
                body: "Use this URL ${BUILD_URL} for more info",
                from: 'pawanks434@gmail.com',
                to: "${GIT_AUTHOR_EMAIL}" 
    }  
   }            
}
