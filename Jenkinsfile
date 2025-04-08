pipeline {
    agent any

    environment {
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-17"
        MVN_HOME = "C:\\Users\\jegan\\OneDrive\\Documents\\Essential Bin Paths\\apache-maven-3.9.9"
        APP_NAME = "Healthcare-App"
        APP_PORT = "8080"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/JeganS21/healthcare-app.git'
            }
        }

        stage('Build') {
            steps {
                bat "\"${MVN_HOME}\\bin\\mvn\" clean package"
            }
        }

        stage('Kill Old Running App') {
            steps {
                bat '''
                for /f "tokens=5" %%a in ('netstat -ano ^| findstr :%APP_PORT%') do taskkill /PID %%a /F
                exit /b 0
                '''
            }
        }

        stage('Deploy New App') {
            steps {
                script {
                    def jarFile = findJar()
                    if (jarFile) {
                        bat '''
                        del app.log
                        start /B java -jar "${jarFile}" > app.log 2>&1
                        '''
                        echo "Application deployed successfully!"
                    } else {
                        error "JAR file not found in target/ directory"
                    }
                }
            }
        }
    }

    post {
        success {
            echo "App running at: http://localhost:${env.APP_PORT}"
        }
        failure {
            echo 'Build or Deploy Failed!'
        }
    }
}

/** Helper to find Jar file **/
def findJar() {
    def files = findFiles(glob: 'target/*.jar')
    return files ? files[0].path : null
}
