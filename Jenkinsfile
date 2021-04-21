pipeline {
     agent any
    stages {
        stage('Checkout') {
            steps {
            checkout scm: [
                    $class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    userRemoteConfigs: [
                        [credentialsId: 'github_moldovan', 
                        url: 'https://github.com/rautate/simple-java-maven-app']
                        ]
                    ]
                }
        }
        stage('Build') { 
            steps {
                withMaven(jdk: 'java-default', maven: 'maven-default') {
                    sh 'mvn -B -DskipTests clean install'
                }
            }
        }
        stage('Test') { 
            steps {
                withMaven(jdk: 'java-default', maven: 'maven-default') {
                    sh 'mvn test' 
                }
            }
        }
        stage('Deploy') { 
            steps {
                withMaven(jdk: 'java-default', maven: 'maven-default') {
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
