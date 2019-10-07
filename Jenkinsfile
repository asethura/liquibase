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
                sh 'mvn install' 
                //archiveArtifacts artifacts: 'target/liquibase-0.0.1-SNAPSHOT.jar'
            }
        }

        stage ('System') {
            steps {
                sh 'ls -R'
                sh 'java -jar -Dspring.profiles.active=sys target/liquibase-0.0.1-SNAPSHOT.jar  ' 
            }
        }

        stage ('Publish') {
            steps {
                sh 'mvn deploy' 
            }
        }

       
    }
}