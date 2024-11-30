pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }

   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=asgbuggywebapp-test_jb-devsecops-test -Dsonar.organization=asgbuggywebapp-test -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=9d775f336a342253461b3b638b1639f11f1a94bb'
			}
        
  }

    stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
