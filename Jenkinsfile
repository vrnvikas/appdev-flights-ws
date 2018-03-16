node
{
    try
		{
			
			//Download code from stash  
    		stage('download_stash_code'){
				download_stash_code()
    		}
			//perform maven clean 
    		stage('clean'){
				clean()
    		}
			//perform maven munit tests     	
			stage('clean') {

				bat 'mvn -U clean test cobertura:cobertura -Dcobertura.report.format=xml'
				junit '**/target/*-reports/TEST-*.xml'
    			step([$class: 'CoberturaPublisher', coberturaReportFile: 'target/site/cobertura/coverage.xml'])
    			
			}
			//perform maven munit tests     	
			stage('sonar_tests'){
				sonar_tests()
			}

			stage('sonar_tests'){
				sonar_tests()
			}

			stage('sonar_tests_coverage'){

				bat 'mvn jacoco:prepare-agent test jacoco:report'
			}

			stage('deploy_to_artifactory'){
				push_to_artifactory()
			}
		
		}
	catch(e) 
		{
		currentBuild.result = "FAILED"	
		throw(e)
		} 
    finally 
		{
			print "done"
		}	
}	
	
// Function definitions start from here 
	
//Function definition for downloading code from Stash to workspace in jenkins 	
def download_stash_code()
	{
	
	checkout scm
	}		
//Function definition to perform maven clean 
def clean()
	{
	bat "mvn clean"
	} 
//Function definition to perform maven tests 	
def munit_tests()
	{
	bat "mvn test"  
	}
//Function definition to perform sonar tests 
def sonar_tests()
{	
	bat "mvn clean sonar:sonar"
}
//Function definition to perform artifactory deploy 
def push_to_artifactory()
{
	bat "mvn deploy"
}







	


	


	
	
	 
