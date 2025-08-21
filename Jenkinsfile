pipeline {
    agent any

    stages {
        stage('Compile and Clean') {
            steps {
                bat 'mvn compile'
            }
        }

        stage('Junit5 Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Jacoco Coverage Report') {
            steps {
                echo 'TestCoverage'
                // jacoco() — enable if plugin is configured
            }
        }

        stage('SonarQube') {
            steps {
                echo 'Sonar Code Scanning'
                // Uncomment and configure if SonarQube is set up
                /*
                sh '''
                mvn sonar:sonar \
                -Dsonar.host.url=http://localhost:9000 \
                -Dsonar.login=<your-sonar-token>
                '''
                */
            }
        }

        stage('Maven Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Docker Diagnostic') {
            steps {
                bat 'docker info'
            }
        }

        stage('Check Docker') {
            steps {
                bat 'docker --version'
            }
        }

        stage('Network Check') {
            steps {
                bat 'curl https://registry-1.docker.io/v2/'
            }
        }

        stage('Docker Test') {
            steps {
                bat 'docker ps'
            }
        }

        stage('Docker Login Secure') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t sampleproject .'
                // Add build args if needed
            }
        }

        stage('Docker Tag') {
            steps {
                bat 'docker tag sampleproject idjdocks/sampleproject:latest'
            }
        }

        stage('Docker Push') {
            steps {
                bat 'docker push idjdocks/sampleproject'
                // Use withCredentials if pushing to private registry
            }
        }

        stage('Docker Deploy') {
            steps {
                bat 'docker run -itd -p 8086:8086 sampleproject'
            }
        }
    }
}
