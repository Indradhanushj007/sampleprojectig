pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/Indradhanushj007/sampleprojectig.git'
            }
        }

        stage('Compile and Clean') { 
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Run Unit Tests') { 
            steps {
                sh 'mvn test'
            }
        }

        stage('Jacoco Coverage Report') {
            steps {
                echo 'Generating Test Coverage Report...'
                // if jacoco plugin integrated, call jacoco()
            }
        }

        stage('SonarQube Analysis'){
            steps {
                echo 'Running SonarQube Code Analysis...'
                // Example if SonarQube server is configured:
                // withSonarQubeEnv('sonar') {
                //     sh 'mvn sonar:sonar'
                // }
            }   
        }

        stage('Maven Build') { 
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Test') { 
            steps {
                sh 'docker ps'
            }
        }

        stage('Build Docker Image'){
            steps {
                sh 'docker build -t sampleproject .'
            }
        }

        stage('Docker Login'){
            steps {
                echo "Logging into DockerHub..."
                // Best practice: use credentials
                // withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                //     sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                // }
            }                
        }

        stage('Docker Tag'){
            steps {
                sh 'docker tag sampleproject idjdocks/sampleproject:latest'
            }                
        }

        stage('Docker Push'){
            steps {
                sh 'docker push idjdocks/sampleproject:latest'
            }
        }

        stage('Docker Deploy'){
            steps {
                sh 'docker run -d -p 8086:8086 --name sampleproject_container sampleproject'
            }
        }
    }
}
