pipeline {
    agent { label 'node1' } 

    stages {
        stage('Delete docker images') {
            steps {
                sh "docker system prune -a"
            }
        }

        stage('Stop and delete docker containers') {
	        steps {
	            sh '''#!/bin/bash
                    docker stop $(docker ps -a -q)
                    docker rm $(docker ps -a -q)
                    '''
            }
        }

        stage('Docker build') {
	        steps {
	            sh "docker build -t homework3 ."       
            }
        }

        stage('Docker run') {
	        steps {
	            sh "docker run -p 8081:80 -d homework3"       
            }
        }

        stage('Test') {
	        steps {
	            sh "curl localhost:8081"       
            }
        }
    }
}
