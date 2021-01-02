pipeline {
	
	agent any
	stages{
		stage('build'){
		  steps{
		  	echo "Build"
		  }
		
		}
		
		stage('test'){
		  steps{
		  	echo "Test"
		  }
		
		}
		
		stage('integration test'){
		  steps{
		  	echo "Integration test"
		  }
		
		}
	}
	
	post{
		always{
			echo "Running always"
		}
		success{
			echo 'Run only after build success'
		}
		failure{
			echo 'Run only after failure'
		}
	}

}
