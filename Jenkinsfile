pipeline {
    agent any // You can specify a specific agent here if needed

    environment {
        // Define any environment variables needed for your build
        JAVA_HOME = '/path/to/your/java/home' // Update with your Java home directory
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code from your version control system (e.g., Git)
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Set up Maven to use your settings.xml if needed
                script {
                    def mvnHome = tool name: 'Maven', type: 'Maven'
                    env.PATH = "${mvnHome}/bin:${env.PATH}"
                }
                
                // Build your project using Maven
                sh 'mvn clean package' // You can adjust the Maven goals as needed
            }
        }

        // Add more stages for additional build and deployment steps as needed
        // For example, you can add stages for testing, packaging, and deploying your application.

        stage('Archive Artifacts') {
            steps {
                // Archive the JAR or WAR file as a build artifact
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
                archiveArtifacts artifacts: '**/target/*.war', allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            // Define actions to take if the build succeeds
            echo 'Build successful!'

            // You can trigger downstream jobs or notifications here if needed
        }

        failure {
            // Define actions to take if the build fails
            echo 'Build failed!'
        }
    }
}
