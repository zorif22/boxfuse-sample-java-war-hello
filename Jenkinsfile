pipeline{
  agent any
   stages{
    stage('Git Cloning'){
	steps{
	 script{
	git branch : 'master', url: 'https://github.com/zorif22/boxfuse-sample-java-war-hello.git'
      }
      }	
    }
	   stage('Unit test'){
		   steps{
			   script{
			   sh 'mvn test'
			   }
		   }
	   }
   
	   stage('Intigration Testing'){
		   steps{
			   script{
			   sh 'mvn verify'
			   }
		   }
	   }
   
	   stage('Build'){
		   steps{
			   script{
			   sh 'mvn clean install'
			   }
		   }
	   }

	   stage('Code Quality test'){
		   steps{
			   script{
			   withSonarQubeEnv(credentialsId: 'boxfuse') {
			   sh 'mvn clean package sonar:sonar'
			   }
			   }
		   }
	   }
		stage('Upload to nexus'){
		   steps{
			   script{
			 	nexusArtifactUploader artifacts:
				   [
					[artifactId: 'javax.servlet-api', 
					classifier: '', 
					file: 'target/hello-1.0.war', 
					type: 'war']
			], 
				credentialsId: '08f0d3b9-1df3-4ea4-854c-d724fe57f197', 
				groupId: 'javax.servlet', 
				nexusUrl: '3.110.152.165:8081',
				nexusVersion: 'nexus3', 
				protocol: 'http', 
				repository: 'boxfuse-sample/', 
				version: '3.1.0' 
	   }
   }
   }
}
}
