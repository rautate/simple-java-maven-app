pipeline {
     agent any
    stages {
        
        stage('Build') { 
            steps {
                withMaven(jdk: 'java-09', maven: 'jenkins-maven') {
                    sh 'mvn -B -DskipTests clean install'
                }
            }
        }
        stage('Test') { 
            steps {
                withMaven(jdk: 'java-09', maven: 'jenkins-maven') {
                    sh 'mvn test' 
                }
            }
        }
        stage('Deploy') { 
            steps {
                withMaven(jdk: 'java-09', maven: 'jenkins-maven') {
                    nexusArtifactUploader artifacts: [
                        [artifactId: 'my-app', 
                        classifier: '', 
                        file: 'target/my-app-1.0-SNAPSHOT.jar', 
                        type: 'jar']], 
                        credentialsId: 'nexus-admin', 
                        groupId: 'com.mycompany.app', 
                        nexusUrl: '192.168.0.84:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', repository: 'maven-snapshots', 
                        version: '1.0-SNAPSHOT'
                   // sh 'mvn deploy -DskipTests' 
                }
            }
        }
    }
}
