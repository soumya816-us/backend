pipeline {
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        //retry(1)
    }
    environment {
        DEBUG = 'true'
        appVersion = '' // this will become global, we can use across pipeline
    }

    stages {
        stage('Read the version') {
            steps {
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "App version: ${appVersion}"

                }

            }
            
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Docker build') {
            steps {

                    sh """
                    docker build -t soumya081693/backend:${appVersion} .
                    docker images
                    """
                    

            }
        }
        
    }

    post {
        always{
            echo "This sections runs always"
            deleteDir()
        }
        success{
            echo "This section run when pipeline success"
        }
        failure{
            echo "This section run when pipeline failure"
        }
    }
}
