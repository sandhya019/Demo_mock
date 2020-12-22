pipeline {
    agent any
    tools {
      maven 'Maven3'
    }
    stages{
        stage('Build'){
            steps{
                sh script: 'mvn clean package'
            }
        }
        stage('Upload jar to Nexus'){
            steps{
                script{
                    def mavenPom = readMavenPom file:'pom.xml'
                    nexusArtifactUploader artifacts: [[
                    artifactId: 'test2',
                    classifier: '',
                    file: "target/*-${mavenPom.version}.jar",
                    type: 'jar']],
                    credentialsId: 'nexus3',
                    groupId: 'org.example',
                    nexusUrl: 'localhost:8081/',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: Demo_repo,
                    version: "${mavenPom.version}"
                }
            }
        }
    }
}