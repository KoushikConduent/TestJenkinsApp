pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''pipeline {
    agent any

    environment {
        ANDROID_HOME = "/path/to/android/sdk" // Adjust the path to your Android SDK
        GRADLE_HOME = "/path/to/gradle" // Adjust the path to your Gradle installation
        PATH = "${env.PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:${GRADLE_HOME}/bin"
    }

    stages {
        stage(\'Checkout\') {
            steps {
                // Checkout the code from the version control system
                git \'https://your.repo.url/your-android-project.git\'
            }
        }
        
        stage(\'Setup\') {
            steps {
                // Install any required dependencies, e.g., using Gradle
                sh \'./gradlew dependencies\'
            }
        }

        stage(\'Build\') {
            steps {
                // Clean and build the project
                sh \'./gradlew clean assembleDebug\'
            }
        }

        stage(\'Test\') {
            steps {
                // Run unit tests
                sh \'./gradlew test\'
                
                // Run instrumentation tests
                sh \'./gradlew connectedAndroidTest\'
            }
        }

        stage(\'Archive\') {
            steps {
                // Archive the build artifacts, e.g., APK files
                archiveArtifacts artifacts: \'**/build/outputs/apk/**/*.apk\', allowEmptyArchive: true
                
                // Optionally, archive test reports
                junit \'**/build/test-results/**/*.xml\'
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
            echo \'Build completed successfully!\'
        }
        failure {
            // Notify failure
            echo \'Build failed!\'
        }
    }
}
'''
        }
      }

    }
  }