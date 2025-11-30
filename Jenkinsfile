pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')   // poll every 1 minute
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat '''
                    echo WORKSPACE=%WORKSPACE%
                    cd src\\hello
                    javac Hello.java
                '''
            }
        }

        stage('Run') {
            steps {
                bat '''
                    cd src\\hello
                    java hello.Hello
                '''
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'src/hello/*.class', fingerprint: true
            }
        }
    }
}
