pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                script {
                    // Remove all files in the current directory before cloning
                    sh 'rm -rf *'
                    
                    // Git clone step
                    sh 'git clone https://github.com/Reddykiram52/kishor-naik-Aaptatt-hiring-assignment.git'
                    
                    // Optional: Print the current working directory for debugging
                    // sh 'pwd'
                }
            }
        }
        stage('Maven Build') {
            steps {
                script {
                    // Maven build step
                    // Optional: Print the current working directory for debugging
                    // sh 'pwd'
                    
                    // Change to the project directory and build
                    dir('/var/lib/jenkins/workspace/aatatt/kishor-naik-Aaptatt-hiring-assignment') {
                        sh 'mvn clean package'
                    }
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    // Docker build step
                    // Change to the project directory and build the Docker image
                    sh 'ls'
                    dir('/var/lib/jenkins/workspace/aatatt/kishor-naik-Aaptatt-hiring-assignment') {
                        sh 'pwd'
                        sh 'docker build -t tomcat:v1 .'
                    }
                }
            }
        }
        stage('Docker Run') {
            steps {
                script {
                    // Change to the project directory and run Docker Compose
                    dir('/var/lib/jenkins/workspace/aatatt/kishor-naik-Aaptatt-hiring-assignment') {
                        sh 'docker-compose up -d'
                    }
                }
            }
        }
    }
}
