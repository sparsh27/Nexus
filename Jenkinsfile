pipeline{
    
    agent any
    environment{
        PATH="/usr/share/maven/bin:$PATH"
    }
    stages{
        
        stage('Scm Checkout'){
            steps{
                
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Github', url: 'https://github.com/sparsh27/new-maven.git']]])
            }
            
            }
        stage('Maven build') {
            
            steps{
                
                sh "mvn clean package"
            }
        } 
        stage('Maven Deploy'){
        
            steps{
                
                nexusArtifactUploader artifacts: [
[
artifactId: 'ILP', 
classifier: '', 
file: 'target/ILP-1.0.war', 
type: 'war'
] 
], 

credentialsId: 'Nexus',
groupId: 'devops.ilp1', 
nexusUrl: 'localhost:8081', 
nexusVersion: 'nexus3', 
protocol: 'http', 
repository: 'Bookstore', 
version: '1.0'
        
            }
        
        }
   
            
        }
    }
