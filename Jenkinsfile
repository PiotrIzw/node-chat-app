pipeline {

    agent any
    	tools{nodejs "NodeJS"}
	
    stages {
        stage('Build') {
            steps {
                echo 'Building!!!'
                sh 'npm install'
        }
            
        post {
         always {
            echo 'Finished!'
         }
         success {
            echo 'Success!'
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                to: 'piotr.izworski.0@gmail.com',
                subject: "Build succeed in Jenkins! :)"
         }
         failure {
            echo 'Failure!'
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                to: 'piotr.izworski.0@gmail.com',
                subject: "Build failed in Jenkins! :("
         }
     	 }
       }
       
        stage('Test') {
            steps {
                echo 'Testing!!!'
		sh 'npm install'
                sh 'npm run test'
            }
		
	post {
		always {
		    echo 'Finished!'
		}
		success {
		    echo 'Success!'
		    emailext attachLog: true,
			body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
			to: 'piotr.izworski.0@gmail.com',
			subject: "Test succeed in Jenkins! :)"
		}
		failure {
		    echo 'Failure!'
		    emailext attachLog: true,
			body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
			to: 'piotr.izworski.0@gmail.com',
			subject: "Test failed in Jenkins! :("
		}
    	}
      }
    }
}
