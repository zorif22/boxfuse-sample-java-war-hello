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
   }
}
