parallel intel: {
	node('intel') {
		stage('Init') {
			echo "completed init on intel"				
		}
        	stage('Build') {	
            		parallel build_client_jars: {                   
				stage('Client JARS') { 						
             	     			echo "completed building client jars on Intel"  
					sleep 60									
				}    
            		},
	    		build_opt: {	
				stage('Build OPT') {
    					echo "completed building OPT on Intel"
       				}
			}
		}
	}
},
power: { 
	node('power') {
  		stage('Init') {
   			echo "completed init on power"    
  		}
        	stage('Build') { 
              		parallel build_client_jars: {                   
    				stage('Client JARS') {       
                      			echo "completed building client jars on Power"  
    				}    
              		},
       			build_opt: { 
    				stage('Build OPT') {
         				echo "completed building OPT on Power"
         	  		}
   			}
  		}
 	}
}
	
