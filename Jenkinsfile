pipeline{
    agent any
    tools {
            maven 'Maven3'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
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
                def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "secondwebapplication-snapshot" : "secondwebapplication-release"
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
                repository: nexusRepoName, 
                version: "${mavenPom.version}"
                }

            }
        }
    }
}
}
