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
                    echo "Image 1: ${params.image1}"
                    echo "Image 2: ${params.image2}"

                    // Upewnij się, że pliki są faktycznie przekazywane
                    if (params.image1 == null || params.image2 == null) {
                        error "One or both file parameters are missing"
                    }
                    
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