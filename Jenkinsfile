pipeline {
    agent any

    environment {
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-17"  // Adjust for your system
        MVN_HOME = "C:\\Users\\jegan\\OneDrive\\Documents\\Essential Bin Paths\\apache-maven-3.9.9\\bin\\mvn"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/JeganS21/healthcare-app.git'
            }
        }

        stage('Build') {
            steps {
                bat '"%MVN_HOME%" clean package'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                start /B java -jar target\\*.jar > app.log 2>&1
                echo %ERRORLEVEL% > app.pid
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
