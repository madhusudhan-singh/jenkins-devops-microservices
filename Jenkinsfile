pipeline {
	
	agent any
	environment{
	
		dockerHome = tool 'myDocker'
		mavanHome = tool 'myMavan'
		PATH = "$dockerHome/bin:$mavanHome/bin:$PATH"
	}
	
	stages{
		stage('Checkout'){
		  steps{
		  		sh 'mvn --version'
			  	sh 'docker --version'
		  		echo "Build"
		  		echo "PATH- $PATH"
		  		echo "BUILD_NUMBER no- $env.BUILD_NUMBER"
		  		echo "BUILD_ID- $env.BUILD_ID"
		  		echo "JOB_NAME- $env.BUILD_JOB_NAME"
		  		echo "BUILD_TAG- $env.BUILD_TAG"
		  		echo "BUILD_URL- $env.BUILD_URL"
		  }
		
		}
		
		stage('Compile'){
		
			steps{
				sh "mvn clean compile"
			}
		}
		/*stage('test'){
		  steps{
		  	sh "mvn test"
		  }
		
		}
		
		stage('integration test'){
		  steps{
		  	sh "mvn failsaif:integration-test failsafe:verify"
		  }
		
		}*/
		
		stage('Package'){
		  steps{
		  	sh "mvn package -DskipTests"
		  }
		
		}
		
		stage('Build docker image'){
			steps{
				script{
					dockerImage = docker.build("madhusudanjim/currency-exchange-service:${env.BUILD_TAG}")
				}
			}
		}
		
		stage('Push docker image'){
			steps{
				script{
					docker.withRegistry('', 'dockerHub'){
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			}
		}
	}
	
}
