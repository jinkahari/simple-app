currentBuild.displayName=  "online-shopping-#"+currentBuild.number
pipeline {
    agent any
    tools {
       maven 'maven'
    }
    stages {
        stage('Build Job'){
            steps {
                sh script: 'mvn clean package'   
            }
        }
    }
}