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
            parallel build_client_jars: {
                    node('power' && 'intel') {                    
			    stage('Client JARS') { 						
             	       		echo "completed building client jars on Power and Intel"  
			    }
		    }
		    
            },
	    build_opt: {
		    node('power && intel') {
			    stage('Build OPT') {
    				  echo "completed building OPT on Power and Intel"
       			    }
		   }
	  }
	}
