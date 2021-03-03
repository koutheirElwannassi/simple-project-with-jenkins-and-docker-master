pipeline {
    agent any
	tools { 
        maven "localMVN" 
        jdk "localJDK" 
    }
    stages {
        stage('Build') {
            steps {
                dir("server/") {
					echo "Build stage and skipping test"
                    bat 'mvn install -DskipTests'
                    
                }
            }
        }
        stage('Junit Tests') {
            steps {
                dir("server/"){
					bat 'mvn test -Dtest=ControllerAndServiceSuite'
					echo "Build Done !!!"
                }
            }
        }
        stage('Deploy') {
            steps {
                bat 'docker-compose build'
                bat 'docker-compose up -d'
            }
        }
        stage('Selenium Tests') {
            steps {
                dir("server/") {
                    bat 'mvn test -Dtest=SeleniumSuite'
                }
            }
        }
    }
}
