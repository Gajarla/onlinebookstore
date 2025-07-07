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

        stage("Debug Target Folder") {
            steps {
                echo "📂 Listing target folder"
                sh 'ls -R target'
            }
        }

        stage("Archive Artifacts") {
            steps {
                echo "📦 Archiving build outputs"
                archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
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
