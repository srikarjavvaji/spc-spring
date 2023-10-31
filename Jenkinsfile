node {
    try {
        stage('Checkout') {
            echo 'Checking out the repository...'
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

        stage('Build') {
            echo 'Building the project...'
            dir('spring-petclinic') {
                sh './mvnw package'
            }
        }

        stage('Run') {
            echo 'Running the application...'
            dir('spring-petclinic') {
                sh 'java -jar -Dserver.port=8081 target/*.jar'
            }
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    } finally {
        archiveArtifacts 'spring-petclinic/target/*.jar'
    }
}
