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
                dir('devsecops-demo') {
                    sh 'mvn clean install -DskipTests'
                }
            }
        }

        stage('Test') {
            steps {
                dir('devsecops-demo') {
                    sh 'mvn test'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    dir('devsecops-demo') {
                        sh '''
                        mvn sonar:sonar \
                          -Dsonar.projectKey=devsecops-demo \
                          -Dsonar.projectName="DevSecOps Demo"
                        '''
                    }
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully. Quality gate passed."
        }
        failure {
            echo "Pipeline failed. Check build logs or SonarQube quality gate."
        }
    }
}

