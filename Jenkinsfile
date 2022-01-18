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
                script{

                def mavenPom = readMavenPom file: 'pom.xml'
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'secondwebapplication', 
                        classifier: '', 
                        file: "target/secondwebapplication-${mavenPom.version}.war", 
                        type: 'war'
                    ]
                ], 
                credentialsId: 'nexus', 
                groupId: 'com.msedcl', 
                nexusUrl: '172.31.98.182:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'secondwebapplication-release', 
                version: "${mavenPom.version}"
                }

            }
        }
    }
}
