	stage('Init') {
		parallel power: {
			node('power') {            	
                		echo "completed init on Power"
			}	
		},
		intel: {
	            	node('intel') {
				echo "completed init on intel"			
			}
		}
	}
        stage('Build') {	
            parallel power: {
                    node('power') {                    
			    stage('Client JARS') { 						
             	       		echo "completed building client jars on Power"  
				sleep 60
			    }
			    stage('Build OPT') {
				echo "completed building OPT on Power"
			    }
		    }
		    
            },
	    intel: {
		    node('intel') {
			    stage('Client JARS') {
				  echo "completed building client jars on Intel"
			    }
			    stage('Build OPT') {
    				  echo "completed building OPT on Intel"
       			    }
		   }
	    }
	}
	stage('DevQA') {
		parallel power: {
			node('power') {
				stage('Basic OPT') {
					echo "Basic OPT on Power Completed"
				}
		}
		intel: {
			node('intel') {
				stage('Basic OPT') {
					echo "Basic OPT on Intel completed"
				}
			}
		}
	}
	
				  
