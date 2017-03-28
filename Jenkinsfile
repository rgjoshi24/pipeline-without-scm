pipeline{
	
	agent{
	     label 'master'
	}

	stages{

		stage('PRINT'){
		
			steps{
			     sh 'echo $JOB_NAME'
			}
		}

		stage('WRITE'){

			steps{
			     sh 'echo $BUILD_NUMBER >> build_number'
			}
		}
		
		stage('Sanity check') {
            			steps {
                			input "Does the staging environment look ok?"
           			 }
        	}
		stage('Code Promotion'){
			steps{
				def userInput = input(id: 'userInput', message: 'Let\'s promote?', parameters: [[$class: 'TextParameterDefinition', defaultValue: 'uat', description: 'Environment', name: 'env'],
 				[$class: 'TextParameterDefinition', defaultValue: 'uat1', description: 'Target', name: 'target']])
				echo ("Env: "+userInput['env'])
				echo ("Target: "+userInput['target'])
			}
		}

		stage('READ'){
		        steps{
			     sh 'cat build_number'
			}
		}
	}

	post{

	    success{
	    	archiveArtifacts artifacts: 'build_number', fingerprint: true 
	    }
	}

}
