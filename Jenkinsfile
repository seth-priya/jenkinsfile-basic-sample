pipeline {
	agent 'intel'
	stages {	
		stage('Init') {
			agent {
				label 'intel'
			}
			steps { 								
				echo "completed init on Intel"
			}
	    	}		
		stage('Build') {
			parallel {
				stage('Client JARS') {
					agent {
						label 'intel'
					}
					steps {
						echo "completed building client jars on Intel"
						sleep 60 												
					}
				}
	    			stage('Build OPT') {
					agent {
						label 'intel'
					}
					steps {
						echo "completed building OPT on Intel"
					}
				}
			}		
	    	}
	    	stage('DevQA') {
			parallel {
				stage('Basic OPT') {
					agent {
						label 'intel'
					}
					steps {
						echo "completed devQA, Basic OPT on Intel"
					}
				}
			}
   		}
	} //end stages
} //end pipeline
