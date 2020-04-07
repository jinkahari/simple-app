currentBuild.displayName=  "online-shopping-#"+currentBuild.number
pipeline {
    agent any
    tools {
        maven 'maven'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages {
        //stage('Build Job'){
            //steps {
                //sh script: 'mvn clean package'   
            //}
        //}
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('jenkins-pipeline-sonar') {
                    // Optionally use a Maven environment you've configured already
                    //withMaven(maven:'Maven 3.7') {
                        sh 'mvn clean package sonar:sonar'
                    //}
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('Upload war to nexus'){
            steps {
                script {
                    def mavenPom = readMavenPom file: 'pom.xml'
                    def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "simpleapp-snapshot" : "simpleapp-release"
                    nexusArtifactUploader artifacts: [
                    [artifactId: 'simple-app', 
                     classifier: '',
                     file: "target/simple-app-${mavenPom.version}.war",
                     type: 'war'
                    ]
                ],
                     credentialsId: 'nexus3',
                     groupId: 'in.javahome',
                     nexusUrl: '172.31.37.76:8081',
                     nexusVersion: 'nexus3', 
                     protocol: 'http', 
                     repository: nexusRepoName, 
                     version: "${mavenPom.version}"
                }   
            }
        }
        stage('Slack Notification') {
            steps{
                slackSend baseUrl: 'https://hooks.slack.com/services/', 
                channel: 'jenkins-pipeline-demo', 
                color: 'good', 
                message: 'Welcome to Slack', 
                teamDomain: '#DevOps', 
                tokenCredentialId: 'slack-demo', 
                username:'jinkahariprasad'
            }    
        }
    }
}
