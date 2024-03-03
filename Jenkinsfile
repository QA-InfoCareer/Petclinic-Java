pipeline {
    agent any
    tools {
        // Define tools like JDK and Maven
        jdk 'jdk11'
        maven 'maven3'
        // SonarQube Scanner tool
        tool 'SonarQube Scanner'
    }
    stages {
        stage('Git Checkout') {
            steps {
                // Checkout code from Git repository
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/your-username/your-repo.git'
            }
        }
        
        stage('Sonar Analysis') {
            steps {
                script {
                    // Run Maven build
                    sh "mvn clean package"
                    
                    // Run SonarQube analysis
                    withSonarQubeEnv('MySonarQubeServer') {
                        sh """
                            ${tool 'SonarQube Scanner'}/bin/sonar-scanner \
                            -Dsonar.projectKey=your-project-key \
                            -Dsonar.sources=src
                        """
                    }
                }
            }
        }
    }
}
