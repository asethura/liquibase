#!groovy
version = '1.1.1'
pipeline {
    agent any
    tools {
        maven 'Maven'
        jdk 'Java'
    }
    stages {
        stage ('Initialize') {
            steps {
                sh  '''
                        echo "PATH = ${PATH}"
                        echo "M2_HOME = ${M2_HOME}"
                    '''
            }
        }

        stage ('Build') {
            steps {
                sh 'mvn install -Dversion=1.1.1-SNAPSHOT' 
            }
        }

        stage ('System') {
            steps {
                sh 'ls -R'
                sh 'java -jar -Dspring.profiles.active=sys target/liquibase-1.1.1-SNAPSHOT.jar' 
            }
        }

        stage ('Release') {
            steps {
                sh 'mvn deploy -Dversion=1.1.1' 
            }
        }

        stage ('Acceptance') {
            steps {
                sh 'curl "http://52.90.38.217:8081/nexus/content/repositories/releases/com/ntrs/liquibase/$version/liquibase-1.1.1.jar" \
     -o liquibase-1.1.1.jar' 
            }
        }

       
    }
}