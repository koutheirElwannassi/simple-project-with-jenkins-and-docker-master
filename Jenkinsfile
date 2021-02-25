pipeline {
    agent any

    stages {
        }
        stage('Build') {
            steps {
                dir("server/"){
                    sh 'mvn install -DskipTests'
                }
            }
        }
        stage('Staging') {
            steps {
                sh 'sudo docker-compose build'
                sh 'sudo docker-compose up -d'
            }
        }
        stage('end2end Tests') {
            steps {
                dir("server/") {
                    sh 'mvn test -Dtest=SeleniumSuite'
                }
            }
        }
    }
}
