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
    }
}
