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
              script {
                 echo 'deploying docker image...'
                 withKubeConfig([credentialsId: 'lke-credentials', serverUrl: 'https://f8b38ba6-680f-4924-87e4-dd6f9ffb2ac5.ap-west-1-gw.linodelke.net']){
                    sh 'kubectl create deployment nginx-deployment --image=nginx'
                 }

                 }
             }

        }
    }
}