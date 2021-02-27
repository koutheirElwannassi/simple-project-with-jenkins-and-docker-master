pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                dir("server/") {
					echo "Build stage and skipping tests"
                    sh 'mvn install -DskipTests'
                    
                }
            }
        }
        stage('Junit Tests') {
            steps {
                dir("server/"){
					sh 'mvn test -Dtest=ControllerAndServiceSuite'
					echo "Build Done !!!"
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose build'
                sh 'docker-compose up -d'
            }
        }
        stage('Selenium Tests') {
            steps {
                dir("server/") {
                    sh 'mvn test -Dtest=SeleniumSuite'
                }
            }
        }
    }
}
