pipeline {                                // declarative pipeline 
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
        // stage('Sonar Scan') { 
        //     steps {
        //         sh 'ls -ltr'
        //         sh 'sonar-scanner'
        //     }
        // }
        stage('Build') { 
            steps {
                sh 'ls -ltr'
                sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip' 
            }
        }
        stage('Publish Artifact') { 
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '54.92.222.103:8081/',
                    groupId: 'com.roboshop',
                    version: '1.0.0',
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth',
                    artifacts: [
                        [artifactId: 'catalogue',
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                ) 
            }
        }
        stage('Deploy') { 
            steps {
                echo "Deployment"
            }
        }
    }
    post{
        always{
            echo 'cleaning up workspace'
            deleteDir()
        }
    }
}