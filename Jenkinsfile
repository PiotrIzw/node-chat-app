#!/usr/bin/env groovy
pipeline {
    agent {
        docker { image 'node:14-alpine' }
    }
    environment{
    	build_success = true
    	
    	
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                
            }
            post {
            	
            	failure{
            		script{
            			build_success = false
            			
            			echo 'Build failed....'
			    	emailext attachLog: true,
				body: "Build failed for job ${env.JOB_NAME}",
				subject: "Build failed.",
				to: 'piotrekizworski@gmail.com'
            		}
            	}
            	success{
            		echo 'Build successful....'
			emailext attachLog: true,
			body: "Builds succeeded for job ${env.JOB_NAME}",
			subject: "Build sucessful.",
			to: 'piotrekizworski@gmail.com'
            	}
            
            }
        }
        stage('Test') {
            steps {
            	script{
            		if(build_success)
            		{
				echo 'Testing..'
				sh 'npm test > tests_log.txt'
			}
                }
            }
            post {
            	
            	success{
            		echo 'Tests succeeded....'
			emailext attachLog: true,
			attachmentsPattern: 'tests_log.txt',
			body: "Tests successful for job ${env.JOB_NAME}",
			subject: "Tests successful.",
			to: 'piotrekizworski@gmail.com'
            	}
            	failure{
            		echo 'Tests failed....'
			emailext attachLog: true,
			attachmentsPattern: 'tests_log.txt',
			body: "Tests failed for job ${env.JOB_NAME}",
			subject: "Tests failed.",
			to: 'piotrekizworski@gmail.com'
            	}
            
            }
            
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
