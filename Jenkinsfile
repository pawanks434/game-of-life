pipeline {
    agent {
       label 'NODE1-JDK8-11-MVN'
       }
       tool {
          jdk 'JDK8_UBUNTU'
       }
    stages {
        stage ('vcs')
            steps {
                git url: 'git@github.com:pawanks434/game-of-life.git'
                branches: 'declarative'
            } 
        }
        stage ('package') {
            steps {
                sh 'mvn package'
            }
        }
        stage ('post build'){
            step {
                archiveArtifacts artifacts: '**/target/gameoflife.war'
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
}