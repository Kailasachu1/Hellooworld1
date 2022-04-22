pipeline {
    agent any
    tools { 
        maven 'Maven_home' 
        jdk 'java_home' 
    }
   
    stages {
        stage ('Initialize') {
            steps {
                bat '''
                    echo "PATH = ${PATH}"
                    echo "MAVEN_HOME = ${MAVEN_HOME}"
                ''' 
            }
        }
        stage('checkout') {
            steps {
                checkout scm
            }
        }
        stage('build') {
            steps {
                bat 'mvn  -B -DskipTests clean package'
            }
        }
        stage('upload to nexus'){
            steps{
                nexusArtifactUploader artifacts: [
                    [
                    artifactId: 'helloworld', 
                    classifier: '', 
                    file: 'target/helloworld-1.0.0.jar', 
                    type: 'jar'
                      ]
                    ], 
                    credentialsId: 'nexus3', 
                    groupId: 'helloworld_sravan', 
                    nexusUrl: 'localhost:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'Test', 
                    version: '1.0.0'
            }
        }
    }
}
    

