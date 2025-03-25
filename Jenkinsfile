pipeline {
    agent any

    environment {
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-17"
        MVN_HOME = "C:\\Users\\jegan\\OneDrive\\Documents\\Essential Bin Paths\\apache-maven-3.9.9"
    }

    stages {
            stage('Checkout') {
                steps {
                    script {
                        echo 'Cloning repository...'
                        git branch: 'main', url: 'https://github.com/your-repo/your-project.git'
                    }
                }
            }

            stage('Build') {
                steps {
                    script {
                        echo 'Building the application...'
                        bat 'mvn clean package -DskipTests'
                    }
                }
            }

            stage('Run Tests') {
                steps {
                    script {
                        echo 'Running unit tests...'
                        bat 'mvn test'
                    }
                }
            }

            stage('Package') {
                steps {
                    script {
                        echo 'Packaging the application...'
                        bat 'mvn clean install'
                    }
                }
            }

            stage('Deploy') {
                steps {
                    script {
                        echo 'Deploying the application...'
                        bat '''
                            for /f "delims=" %%i in ('dir /b target\\*.jar') do set JAR_FILE=%%i
                            echo Deploying %JAR_FILE%...
                            copy target\\%JAR_FILE% C:\\deploy\\
                        '''
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