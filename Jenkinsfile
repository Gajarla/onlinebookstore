pipeline {
    agent any

    environment {
        MAVEN_OPTS = "-Dmaven.test.failure.ignore=true"
    }

    stages {
        stage("Git Checkout") {
            steps {
                echo "🔄 Cloning repository"
                checkout scm
                echo "✅ Repo cloned successfully"
            }
        }

        stage("Build with Maven") {
            steps {
                echo "🔨 Starting Maven build"
                sh 'mvn clean package'
            }
        }

        stage("Debug Workspace") {
            steps {
                echo "🧭 Listing all files in workspace"
                sh 'find . -type f'
            }
        }

        stage("Archive Artifacts") {
            steps {
                echo "📦 Trying to archive all JARs"
                archiveArtifacts artifacts: '**/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Check build logs."
        }
    }
}
