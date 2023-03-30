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
   }
}
