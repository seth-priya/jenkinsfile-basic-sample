        stage('Init') {
		node('power') {            	
                	echo "completed init on Power"
		}  						
            }
        stage('Build') {
            parallel {
                stage('Client JARs') {
                    node('power') {                    
                        echo "completed building client jars on Power"                    			    
		    }									
                }
                stage('Build OPT') {
                    node('power') {
		         echo "completed building OPT on Power"			
		    }                  						
                }
	    }
		
	}	
