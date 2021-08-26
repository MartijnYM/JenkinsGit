pipeline {
    environment {
        registry = 'israelaminu/ml_model'
        registryCredential = 'martijnym/testing_ml:tagname'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Build Docker Image') {
            agent any
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
		stage('Testing ML') {
			agent any
			steps {
				echo 'Testing time'
				sh 'docker ps'
				sh 'docker exec -it $registry:$BUILD_NUMBER curl localhost:9090'
				sh 'curl localhost:9090'
				echo 'Done testing'
			}
		}
        stage('Remove Unused docker image') {
            steps {
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}