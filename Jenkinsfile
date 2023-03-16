pipeline {
    agent any
    triggers { pollSCM('30 22 * * 1-5') }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/pawanks434/game-of-life.git',
                branch: 'dev'
            }
        }
        stage(package) {
                tools {
                    jdk 'JDK8_UBUNTU'
                }
                 steps {
                    sh  'mvn package'
                 }   
        }
    }  
}