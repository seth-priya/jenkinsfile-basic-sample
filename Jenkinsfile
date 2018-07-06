pipeline {
	agent none
	stages {
	    	stage('Init') {
			parallel {
				stage('Power Init') {  							
					agent {
						label 'power'
					}
					steps { 								
						echo "completed init on Power"
					}
 		    		}
				stage('Intel init') {
					agent {
						label 'intel'
					}
					steps {
						echo "completed init on Intel"
					}
				}
			}		
			
		} 			
			stage('Build') {
						parallel {
						stage('Client JARS') {
							agent {
								label 'power'
								}
							steps {
								echo "completed building client jars on Power"
								sleep 60 												
							}
						}
			    			stage('Build OPT') {
							agent {
								label 'power'
							}
							steps {
								echo "completed building OPT on Power"
							}
						}
					}		
			    	}
			    	stage('DevQA') {
					parallel {
						stage('Basic OPT') {
							agent {
								label 'power'
							}
							steps {
								echo "completed devQA, Basic OPT"
							}
						}
					}
		   		}
			//} //end parallel
	    	// } //end parallel stage
	} //end stages
} //end pipeline
