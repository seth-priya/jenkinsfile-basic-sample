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
                stage('Client JARs') {
                    agent {
                        label 'power'
		    }
                    steps {
                        echo "completed building client jars on Power"
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
