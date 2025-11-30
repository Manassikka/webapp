pipeline {
    agent any   // run on any available node

    stages {

        stage('Build') {
            steps {
                // Build the project and skip tests
                bat 'mvn -B -DskipTests clean package'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                bat 'mvn test'
            }
            post {
                always {
                    // Publish JUnit test reports
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        // SonarQube is disabled because server is not running
        // stage('Sonar-Report') {
        //     steps {
        //         bat 'mvn clean install sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.analysis.mode=publish'
        //     }
        // }
    }
}
