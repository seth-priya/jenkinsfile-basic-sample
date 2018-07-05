        stage('Init') {
		node('power') {
            		steps {
                		echo "completed init on Power"
                	}
		}  						
            }
        stage('Build') {
            parallel {
                stage('Client JARs') {
                    node('power') {
                    	steps {
                        	echo "completed building client jars on Power"
                    	}			    
		    }									
                }
                stage('Build OPT') {
                    node('power') {
                        steps {
		         echo "completed building OPT on Power"			
                        }
		    }                  						
                }
	    }
		
	}	
