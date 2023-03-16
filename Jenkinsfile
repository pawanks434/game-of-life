pipeline {
    agent any
    trigger { pollSCM ('* * * * *') }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/pawanks434/game-of-life.git',
                branch: 'master'
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