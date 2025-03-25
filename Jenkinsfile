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
                    git branch: 'main', url: 'https://github.com/JeganS21/healthcare-app.git'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building the application...'
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    echo 'Running unit tests...'
                    sh 'mvn test'
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    echo 'Packaging the application...'
                    sh 'mvn clean install'
                }
            }
        }

        stage('Approve Script Permissions') {
            steps {
                script {
                    echo 'Approving script permissions...'
                    sh 'echo "new java.io.File java.lang.String" >> /var/jenkins_home/approved-signatures'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying the application...'
                    sh '''
                        JAR_FILE=$(ls target/*.jar | head -n 1)
                        echo "Deploying $JAR_FILE..."
                        cp $JAR_FILE /opt/app/
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
