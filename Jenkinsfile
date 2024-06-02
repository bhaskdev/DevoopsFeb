pipeline {
    agent any

    tools {
        // Specify Maven tool installation
        maven 'Default Maven'
    }
    environment {
        SONARQUBE_ENV = 'SonarQube' // Replace with your SonarQube installation name
    }

    stages {
        stage('git checkout') {
            steps {
                // Checkout the repository
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/OpqTech/java-onlinebookstore.git']])
            }
        }
        
        stage('Build') {
            steps {
                // Build the Maven project
                sh "mvn clean package"
            }
        }
  stage('SonarQube Analysis') {
      steps {
    script {
                    def mvn = tool 'Default Maven'
                }
          
    withSonarQubeEnv(installationName: 'SonarQube') {
        script {
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=opqdemo"
          }
    }
  }
  }
}
}
