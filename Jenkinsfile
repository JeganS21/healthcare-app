pipeline {
    agent any

    environment {
        JAVA_HOME = "C:\Program Files\Java\jdk-17"  // Adjust for your system
        MVN_HOME = "C:\Users\jegan\OneDrive\Documents\Essential Bin Paths\apache-maven-3.9.9\bin\mvn"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/JeganS21/healthcare-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                nohup java -jar target/*.jar > app.log 2>&1 &
                echo $! > app.pid
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
