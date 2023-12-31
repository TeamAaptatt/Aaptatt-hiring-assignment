pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                script {
                    // Clean the workspace before cloning
                    deleteDir()
                    
                    // Git clone step
                    sh 'git clone https://github.com/Reddykiram52/kishor-naik-Aaptatt-hiring-assignment.git'
                    
                    // Print the current working directory for debugging
                    sh 'pwd'
                }
            }
        }

        stage('Maven Build') {
            steps {
                script {
                    // Change to the project directory and build with Maven
                    dir('kishor-naik-Aaptatt-hiring-assignment') {
                        sh 'mvn clean package'
                    }
                }
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    // Change to the project directory and build the Docker image
                    dir('kishor-naik-Aaptatt-hiring-assignment') {
                        sh 'docker build -t tomcat:v1 .'
                    }
                }
            }
        }

        stage('Docker Run') {
            steps {
                script {
                    // Change to the project directory and run Docker Compose
                    withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
                        dir('kishor-naik-Aaptatt-hiring-assignment') {
                            sh 'docker-compose down'
                            sh 'docker-compose up -d'
                        }
                    }
                }
            }
        }

        stage('Clone VM') {
            steps {
                script {
                    // Push the Docker image to the registry
                    withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
                        sh 'docker tag tomcat:v1 reddykiram52/tomcat:v1'
                        sh 'docker push reddykiram52/tomcat:v1'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
