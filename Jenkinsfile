#!/usr/bin/env groovy

pipeline {
    agent any
    stages {
        stage('build app') {
            steps {
               script {
                   echo "building the application..."
               }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "building the docker image..."
                }
            }
        }
        stage('deploy') {
            steps {
                withCredentials([
                                string(credentialsId: 'jenkins_aws_access_key_id', variable: 'AWS_ACCESS_KEY_ID'),
                                string(credentialsId: 'jenkins-aws_secret_access_key', variable: 'AWS_SECRET_ACCESS_KEY')
                            ]) {
                script {
                   echo 'deploying docker image...'
                   echo "AWS Access Key ID: ${env.AWS_ACCESS_KEY_ID}"
                   sh 'echo "AWS Access Key ID: $AWS_ACCESS_KEY_ID"'
                            // Test AWS credentials
                    sh 'aws sts get-caller-identity'
                   sh 'aws-iam-authenticator token -i demo-cluster'
                   sh 'kubectl create deployment nginx-deployment --image=nginx'
                }
                }
            }
        }
    }
}