pipeline{

	agent {label 'linux'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/shazforiot/nodeapp_test.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t awadeisa/test1:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push awadeisa/test1:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
