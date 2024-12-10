pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Adunius/sp-lab4.git', credentialsId: 'add credentialsId'
            }
        }
        
        stage('Build') {
            steps {
                script {
                    try {
                        bat '"C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" pozdniakov-test.sln /p:Configuration=Debug /p:Platform=x64 /m'
                    } catch (Exception e) {
                        echo "Build error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to build failure.")
                    }
                }     
            } 
        }   
            
        stage('Test') {
            steps {
                script {
                    try {
                        bat "P:\\lab4 kyrs\\pozdniakov-test\\x64\\Debug\\pozdniakov-test.exe"'
                    } catch (Exception e) {
                        echo "Test error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to test execution failure.")
                    }
                }
            }
        }
    }

    post {
         always {
             cleanWs()
         }
         
         failure {
             echo "Pipeline failed. Check logs to fix the issues."
         }
         
         success {
             echo "Pipeline completed successfully!"
         }
     }
 }   
        