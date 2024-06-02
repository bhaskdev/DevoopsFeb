pipeline {
    agent any

    tools {
        // Specify Maven tool installation
        maven 'Default Maven'
    }
    environment{
        SCANNER_HOME= tool 'sonar'
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
     mvn = tool 'Default Maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=opqdemo"
    }
  }
  }
}
}
