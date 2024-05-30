pipeline {
    agent any

    environment {
        ANDROID_HOME = "C:\\Users\\52406870\\AppData\\Local\\Android\\Sdk"
        PATH = "${env.PATH}:${ANDROID_HOME}\\tools:${ANDROID_HOME}\\platform-tools"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the version control system
                git 'https://github.com/KoushikConduent/TestJenkinsApp.git'
            }
        }
        
        stage('Setup') {
            steps {
                // Install any required dependencies, e.g., using Gradle
                sh './gradlew dependencies'
            }
        }

        stage('Build') {
            steps {
                // Clean and build the project
                sh './gradlew clean assembleDebug'
            }
        }

        stage('Archive') {
            steps {
                // Archive the build artifacts, e.g., APK files
                archiveArtifacts artifacts: '**/build/outputs/apk/**/*.apk', allowEmptyArchive: true
                
                // Optionally, archive test reports
                junit '**/build/test-results/**/*.xml'
            }
        }
    }

    post {
        always {
            // Clean up workspace after build
            cleanWs()
        }
        success {
            // Notify success
            echo 'Build completed successfully!'
        }
        failure {
            // Notify failure
            echo 'Build failed!'
        }
    }
}
