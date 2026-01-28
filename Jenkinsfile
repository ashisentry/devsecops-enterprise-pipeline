pipeline {
    agent { label 'linux' }

    tools {
        jdk 'jdk'
        maven 'mvn'
    }

    stages {
        stage('Checkout') {
            steps {
              checkout scm 
            }
        }

        stage('Build') {
            steps {
		dir('devsecops-demo'){
			sh 'mvn clean install'
		}
            }
        }

        stage('Test') {
            steps {
		dir('devsecops-demo'){
                sh 'mvn test'
        	    }
		}
        }
    }

    post {
        success {
            echo "Build Successful"
        }
        failure {
            echo "Build Failed"
        }
    }
}

