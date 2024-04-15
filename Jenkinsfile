#!groovy
pipeline {
    environment {
        registry = 'sanandsan/jenkinsbuild'
        dockerCred = 'dock-creds'
    }
    agent any
    stages {
        stage('Cloning git repository') {
            steps {
            git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/sanjayaradya/sanandsan.git'
            }
        }
        stage('Building an Image') {
            steps {
                sh 'Image build starts'
                script {
                    image = docker.build("${registry}:$BUILD_NUMBER")
                }
            }
            
        }
        stage('Pushing an image to registry') {
            steps {
                sh 'Pushing an image starts'
                script {
                    docker.withRegistry('', dockerCred){
                        image.push()
                        image.push(latest)
                    }
                }
            }
        }
    }
}
