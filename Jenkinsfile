pipeline {
	agent none
	stages {
		stage('parallel') {
			parallel {	
		//		stage('Power') {
		//			agent {
		//				label 'power'
		//			}
		//			steps {
		//				echo "executing power stage"
		//			}
			    		stage('Init') {
						agent {
	 						label 'power'
						}
						steps { 								
							echo "completed init on Power"
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
		      	//	} //end power stage
			//	stage('Intel') {
			//		agent {
			//			label 'intel'
			//		}
			//		steps {
			//			echo "Intel stage triggered"
			//		}
		     	//	} //end intel stage
			} //end parallel
	    	} //end parallel stage
	} //end stages
} //end pipeline
