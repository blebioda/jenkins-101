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
                unstash 'image1'
                unstash 'image2'

                sh 'mv image1 $image1_FILENAME'
                sh 'mv image2 $image2_FILENAME'
            }
        }
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                python3 -m pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                python3 logo_changer.py
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
}