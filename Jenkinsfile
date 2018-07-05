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
                    node('power && intel') {                    
			    stage('Client JARS') { 						
             	       		echo "completed building client jars on Power"  
				sleep 60
			    }
			    stage('Build OPT') {
				echo "completed building OPT on Power"
			    }
		    }
	}
				  
