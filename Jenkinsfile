pipeline {
    agent {
        docker {
            image 'maven:3.5.3'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
               sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
		stage('Build docker image') {
            steps {
                node {
						checkout scm
						def customImage = docker.build("my-image:${env.BUILD_ID}")
						customImage.push()

						customImage.push('latest')
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
