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
				stage('Power Client JARS') {
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
				} //end Power Client JARS stage
				stage('Intel Client JARS') {
					parallel {
						stage('Client JARS') {
							agent {
								label 'intel'
							}
							steps {
								echo "completed building client jars on Intel"
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
				} //end Intel Client JARS
			} //end parallel 						
		} //end Build stage									    	}
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
	} //end stages
} //end pipeline
