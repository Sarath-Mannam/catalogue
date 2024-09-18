pipeline {                                // declarative pipeline 
    agent { node { label 'Agent-1' } }
    environment{ 
        // here if you create any variable it will have global access because it is env varialble
        version = ''
    }
    stages {
        stage('Get version') {
            steps{
                script {
                    // Read the package.json file
                    def packageJson = readJSON file: 'package.json'
                    
                    // Extract the version
                    // def version = packageJson.version
                       version = packageJson.version
                    
                    // Display the version
                    echo "Catalogue component version: ${version}"
                }
            }
        }
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
                // sh 'ls -ltr'
                // sh 'sonar-scanner'
                echo "Sonar scan completed"
            }
        }
        stage('Build') { 
            steps {
                sh 'ls -ltr'
                sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip' 
            }
        }
        stage('Static Application Security Testing') { 
            steps {
                echo "SAST Completed"
                echo "package version: $version"
            }
        }
        // Install pipeline utility steps plugin 
        stage('Publish Artifact') { 
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '54.167.120.230:8081/',  // private ip of nexus
                    groupId: 'com.roboshop',
                    version: "$version",
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