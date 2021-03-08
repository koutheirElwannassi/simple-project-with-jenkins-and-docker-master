pipeline {
    agent any
	tools { 
        maven "localMVN" 
        jdk "localJDK" 
    }
    stages {
        stage('Junit Tests') {
            steps {
                dir("server/"){
					bat 'mvn test -Dtest=ControllerAndServiceSuite'
					echo "Tests Done !!!"
                }
            }
        }
		stage('Integration Tests') {
            steps {
                dir("server/"){
					bat 'mvn test -Dtest=IntegrationSuite'
					echo "Tests Done !!!"
                }
            }
        }
		stage('Build/Majed') {
            steps {
                dir("server/") {
                    bat 'mvn install -DskipTests'
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
        stage('end2end-Selenium Tests') {
            steps {
                dir("server/") {
                    bat 'mvn test -Dtest=SeleniumSuite'
                }
            }
        }
    }
}
