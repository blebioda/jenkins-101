pipeline {
    agent { 
        node {
            label 'docker-agent-python'
            }
      }
    parameters {
        stashedFile(name: 'image1', description: 'Upload the first image file')
        stashedFile(name: 'image2', description: 'Upload the second image file')
    }
    stages {
        stage('Prepare') {
            steps{
                sh 'mkdir logos'
                unstash 'image1'
                unstash 'image2'

                sh 'mv image1 ./logos/$image1_FILENAME'
                sh 'mv image2 ./logos/$image2_FILENAME'
            }
        }
        stage('Install requirements') {
            steps {
                echo "Building.."
                sh '''
                python3 -m pip install --upgrade pip
                pip install -r requirements.txt
                apk add zip
                '''
            }
        }
        stage('Generate') {
            steps {
                echo "Generating.."
                sh '''
                python3 logo_changer.py
                '''
            }
        }
        stage('Archive') {
            steps {
                echo 'Archiving....'
                sh '''
                zip -r logos.zip logos
                '''
                archiveArtifacts artifacts: 'logos.zip', fingerprint: true
            }
        }
    }
    post {
        always {
            script {
                def downloadUrl = "${env.BUILD_URL}artifact/logos.zip"
                echo "Download the ZIP file from: ${downloadUrl}"
            }
        }
    }
}