pipeline {
    agent any
    tools {
      maven 'Maven3'
    }
    stages{
        stage("Maven Build") {
            steps {
                script {
                    sh "mvn package -DskipTests=true"
                }
            }
        }
        stage('Upload jar to Nexus'){
            steps{
                script{
                    pom = readMavenPom file: "pom.xml";
                    nexusArtifactUploader artifacts: [[
                    artifactId: pom.artifactId,
                    classifier: '',
                    file: "target/*-${pom.version}.jar",
                    type: 'jar']],
                    credentialsId: 'nexus3',
                    groupId: pom.groupId,
                    nexusUrl: 'localhost:8081/',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: Demo_repo,
                    version: pom.version
                }
            }
        }
    }
}
