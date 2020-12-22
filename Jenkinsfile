pipeline {
    agent any
    tools {
      maven 'Maven3'
    }
    
     environment {
         NEXUS_REPOSITORY = "maven-releases"
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
                    nexusUrl: 'localhost:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'mock2_repo',
                    version: pom.version
                }
            }
        }
    }
}

 post {
	always {
		script {
            emailext body: '<h4> ${currentBuild.currentResult}: </h4> Job: <h4> ${env.JOB_NAME}</h4> build: <h4>${env.BUILD_NUMBER}</h4>', 
                subject: 'Build status', 
                to: 'sandhyareddy019@gmail.com'
        }
    }
 }
