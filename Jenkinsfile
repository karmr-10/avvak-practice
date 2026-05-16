pipeline {

    agent any

    tools {

        jdk 'jdk21'
        nodejs 'node20'
    }

    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {
        stage('clean workspace') {
            steps{
                cleanws()
            }
        }

        stage('checkout from git'){
            steps{
                git branch: 'main',
                    url: 'https://github.com/karmr-10/avvak-practice.git'
            }
        }

        stage('Install Dependencies'){
            steps{
                sh 'npm install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh '''
                        $SCANNER_HOME/bin/sonar-scanner \
                        -Dsonar.projectKey=pani-practice \
                        -Dsonar.projectName=pani-practice \
                        -Dsonar.sources=.
                    '''
                }
            }
        }
    }
}

    