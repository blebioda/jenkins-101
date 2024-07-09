pipeline {
    agent { 
        node {
            label 'docker-agent-python'
            }
      }
    parameters {
        file(name: 'icon', description: 'icon file')
        file(name: 'logo', description: 'logo file')
    }
    stages {
        stage('Prepare') {
            steps{
                script {
                    sh "cp ${params.icon} ./logos/image1.png"
                    sh "cp ${params.logo} ./logos/image2.png"
                }
            }
        }
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
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