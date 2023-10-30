pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    def projectDir = 'spring-petclinic'
                    if (fileExists(projectDir)) {
                        echo "Directory $projectDir already exists. Updating the repository."
                        dir(projectDir) {
                            sh 'git pull'
                        }
                    } else {
                        echo "Cloning the Git repository."
                        sh 'git clone https://github.com/spring-projects/spring-petclinic.git'
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    dir('spring-petclinic') {
                        sh './mvnw package'
                    }
                }
            }
        }

        stage('Run') {
            steps {
                script {
                    dir('spring-petclinic') {
                        sh 'java -jar -Dserver.port=8081 target/*.jar'
                    }
                }
            }
        }
    }
}
