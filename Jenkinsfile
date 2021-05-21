pipeline {
    agent any
tools {nodejs "node" }
    stages {
        stage('Git Clone') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/swetasgit/webapp.git'
                          }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
        steps {
               echo "sh 'npm test'"
                       }
               }
               
        stage('Building image') {
        steps{
            sh 'sudo docker build . -t docswe/node-web-app'
                }
        }
		stage('Deploy') {
		steps{
		    script {
            withDockerRegistry(credentialsId: 'test', toolName: 'docker', url: 'https://hub.docker.com/repository/docker/docswe/dockerapp') {
            def customImage = docker.build("docswe/node-web-app")
			customImage.push()
            }
             }
            
            }
      }
    }
	}
