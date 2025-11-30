pipeline {
    agent any   // run on any available agent/node

    stages {

        stage('Build') {
            steps {
                // Build the project and skip tests during this phase
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
                    // Publish JUnit test reports in Jenkins
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Sonar-Report') {
            steps {
                // Run SonarQube analysis
                // NOTE: SonarQube must be running on http://localhost:9000
                bat 'mvn clean install sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.analysis.mode=publish'
            }
        }
    }
}
