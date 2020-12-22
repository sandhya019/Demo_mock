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
               	nexusArtifactUploader artifacts: [[
			artifactId: 'test2', 
			classifier: '', 
			file: 'target/test2-1.0.8.jar', 
			type: 'jar']], 
			credentialsId: 'Nexus_id', 
			groupId: 'org.example', 
			nexusUrl: 'localhost:8081', 
			nexusVersion: 'nexus3', 
			protocol: 'http', 
			repository: 'mock2_repo', 
			version: '1.0.8'
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
