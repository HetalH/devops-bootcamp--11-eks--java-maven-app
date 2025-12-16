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
                  sh 'aws eks update-kubeconfig --name demo-cluster --region us-east-1'

                                       // Verify AWS IAM authentication works
                                       sh 'aws sts get-caller-identity'

                                       // kubectl will automatically use aws-iam-authenticator
                                       sh 'kubectl get nodes'

                                       // Deploy a test app
                                       sh 'kubectl create deployment nginx-deployment --image=nginx'
                }
                }
            }
        }
    }
}