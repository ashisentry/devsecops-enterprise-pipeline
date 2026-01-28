pipeline {
    agent { label 'linux' }

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ashisentry/devsecops-enterprise-pipeline.git'
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

