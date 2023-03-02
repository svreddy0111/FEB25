pipeline{
	agent any
	stages{
		stage('APPBUILD')
		{
		  steps{
			sh '''
				pwd
				ls -l
				cd App
				
				cd target
				ls -l 
			'''
		   }	
		}
		stage('IMAGEBUILD')
		{
			steps {
				sh """
			    pwd
			    cd K8s
			    cp ../App/target/*.jar .
			    ls -l 
			    docker build -t webapp:v${BUILD_NUMBER} .
				docker images
			"""
			}
		}
		stage('Deployk8s')
		{
			steps {
				sh """
				 cd K8s
			     sed -i "s/IMAGE_REP/docker.io\\/sheshivardhan28\\/webapp:${BUILD_NUMBER}/" Deployment.yml
				 cat Deployment.yml
			"""
			}
		}
		
	}
}
