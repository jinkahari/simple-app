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
        //stage('Upload war to nexus'){
          //  steps {
            //    nexusArtifactUploader artifacts: [
              //      [artifactId: 'simple-app', 
                //     classifier: '',
                  //   file: 'target/simple-app-1.0.0.war',
                   //  type: 'war'
                   // ]
                //],
                 //    credentialsId: 'nexus3',
                   //  groupId: 'in.javahome',
                   //  nexusUrl: '172.31.37.76:8081',
                    // nexusVersion: 'nexus3', 
                    // protocol: 'http', 
                   //  repository: 'simpleapp-release', 
                   //  version: '1.0.0'   
            //}
        }
    }
}
