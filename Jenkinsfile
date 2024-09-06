pipeline {
    agent { node { label 'Agent-1' } }
    stages {
        stage('Install dependencies') { 
            steps {
                sh 'npm install'
            }
        }
        stage('Unit test') { 
            steps {
                echo "unit testing is done"
            }
        }
        // sonar-scanner command expect sonar-project.properties file has to be available
        stage('Sonar Scan') { 
            steps {
                sh 'ls-ltr'
                sh 'sonar-scanner'
            }
        }
    }
}