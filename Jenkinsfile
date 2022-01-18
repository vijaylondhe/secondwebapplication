pipeline{
    agent any
    tools {
            maven 'Maven3'
    }
    stages{
        stage("Build"){
            steps{
                sh 'mvn clean package'
            }

        }
        stage("Upload to Nexus"){
            steps{
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'secondwebapplication', 
                        classifier: '', 
                        file: 'target/secondwebapplication-0.0.1.war', 
                        type: 'war'
                    ]
                ], 
                credentialsId: 'nexus', 
                groupId: 'com.msedcl', 
                nexusUrl: '172.31.98.182:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'secondwebapplication-release', 
                version: '0.0.1'
            }
        }
    }
}
