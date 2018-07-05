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
			    }						
		    }
		    
            },
	    intel: {
		    node('intel') {
			    stage('Client JARS') {
				  echo "completed building client jars on Intel"
			    }
		   }
	  }
	}
				  
				  
                //stage('Build OPT') {
                  //  node('power') {
		    //     echo "completed building OPT on Power"			
		    //}                  						
                //}
	    //}
		
	//}	
