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
stage('upload to nexus'){
		   steps{
			   script{
			 [
					[
					artifactId: 'javax.servlet-api', 
					classifier: '', 
					file: 'target/hello-1.0.war', 
					type: 'war'
				]
			], 
					credentialsId: 'nexus', 
					groupId: 'javax.servlet', 
					nexusUrl: '3.110.152.165:8081',
					nexusVersion: 'nexus3', 
					protocol: 'http:// http://3.110.152.165:8081/', 
					repository: 'boxfuse-sample/', version: '3.1.0' 
	   }
   }
   }
}
}
