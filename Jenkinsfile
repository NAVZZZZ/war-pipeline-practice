
pipeline {
    agent any

    tools {
        jdk 'jdk-21'
        maven 'maven-ci-server'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/war-pipeline-practice.war',
                                 fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                deploy(
                    adapters: [
                        tomcat9(
                            credentialsId: 'jenkinsdeploy-tomcat',
                            url: 'http://54.87.201.69:8080'
                        )
                    ],
                    contextPath: '/myapp',
                    war: 'target/war-pipeline-practice.war'
                )
            }
        }
    }
}
