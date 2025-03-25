pipeline {
    agent any

    environment {
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-17"
        MVN_HOME = "C:\\Users\\jegan\\OneDrive\\Documents\\Essential Bin Paths\\apache-maven-3.9.9"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/JeganS21/healthcare-app.git'
            }
        }

        stage('Build') {
            steps {
                bat '%MVN_HOME%\\bin\\mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def jarFile = getJarFile()
                    if (jarFile) {
                        echo "Deploying ${jarFile}..."
                        bat "start /B java -jar \"${jarFile}\" > app.log 2>&1"
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
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

/** Find the JAR file inside the target directory **/
def getJarFile() {
    def jarFile = ''
    def output = bat(script: 'for /F "delims=" %%i in (\'dir /b target\\*.jar\') do @echo %%i', returnStdout: true).trim()
    if (output) {
        jarFile = "target\\" + output
    }
    return jarFile
}
