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
		
		stage('Toll Gate'){
			steps{
				def doesJavaRock = input(message: 'Do you like Java?', ok: 'Yes',parameters: [booleanParam(defaultValue: true,description: 'If you like Java, just push the button',name: 'Yes?')])
				echo "Java rocks?:" + doesJavaRock
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
