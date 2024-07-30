pipeline {
    environment {
        imagename = 'jeenaprem/devops-integration'
        registryCredential = 'github-username-pwd'
        dockerImage = ''
    }
    agent any
    tools {
        maven 'maven_3_9_8'
    }
    stages{
        stage('Build using Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jeenlearn/devops-automation']])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t jeenaprem/devops-integration .'
                }
            }
        }
       stage('Push image to dockerhub'){
            steps{
                script{
                    docker.withRegistry( '', registryCredential )   {
                    bat 'docker push jeenaprem/devops-integration'
                    }
                }
            }
        }
    }
}