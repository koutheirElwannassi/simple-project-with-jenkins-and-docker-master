pipeline {
    agent any

    stages {
        stage('Testing Environment') {
            steps ('Junit-Tests'){
                dir("server/") {
                    bat 'mvn test -Dtest=ControllerAndServiceSuite'
                    
                }
            }
			steps ('Integration-Tests'){
                dir("server/") {
                    bat 'mvn test -Dtest=IntegrationSuite'
                }
            }
        }
        stage('Build') {
            steps {
                dir("server/"){
                    bat 'mvn install -DskipTests'
                }
            }
        }
        stage('Staging') {
            steps('Building-The-Image') {
                bat 'sudo docker-compose build'
            }
			steps('Running-The-Image') {
                bat 'sudo docker-compose up -d'
            }
        }
        stage('end2end Tests') {
            steps('Selenium-Tests') {
                dir("server/") {
                    sh 'mvn test -Dtest=SeleniumSuite'
                }
            }
        }
    }
}