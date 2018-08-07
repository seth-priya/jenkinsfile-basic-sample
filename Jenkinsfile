def builders = [:]

def getEngineBuildArchChoices() {
    // To avoid racing conditions being obscured by ASAN tests, run OPT by default as well
    return "intel\npower\nintel,power"
}

def doInit(arch, buildMode) {
	echo "In init BuildMode=${buildMode}, Architecture=${arch}"
}

def doBuild(arch, buildMode) {
        echo "In Build BuildMode=${buildMode}, Architecture=${arch}"
}

pipeline {
	agent none
	parameters {
		choice(choices: getEngineBuildArchChoices(),
                description: 'What architecture to run build/test on?',
                name: 'engineBuildAndTestArch')
	}
	stages {
		stage('Init') {
			steps {
				script {
				       def archs = params.engineBuildAndTestArch.split(",")
				       for (x in archs) {				
					    def arch = x
					    builders["${arch} Init"] = {
						def nodeLabel = (arch == "intel") ? "welterweight" : "welter${arch}"
						node(nodeLabel) {
							doInit(arch, 'OPT')
						}
					    }
					}	
					parallel builders
				}			
			}
		}
		stage('Build') {
			when {
				expression { params.engineBuildAndTestArch.contains('x86_64') == true }
			}
			parallel {
				stage('Client JARS') {
	      	                    steps {
                	                script {
                        	            def archs = params.engineBuildAndTestArch.split(",")
                                	        for (x in archs) {
                                        	    def arch = x
                                           	    builders["${arch} Client JARS"] = {
                                      		        def nodeLabel = (arch == "intel") ? "welterweight" : "welter${arch}"
                                                	node(nodeLabel) {
                                                            doBuild(arch, 'OPT')
                                            	        }
                                        	    }
						}
                                             parallel builders
                                	}
				    }
                        	}
				stage('Intel Build OPT') {
					agent {
						label 'intel'
					}
					steps {
						echo "Running Build OPT on Intel"
					}
				}
				stage('Power Build OPT') {
					agent {
						label 'power'
					}
					steps {
						echo "Running Build OPT on Power"
						echo "Sleeping for 60 seconds ..."
						sleep 60						
					}
				}
				stage('Intel Build ASAN') {
					agent {
						label 'intel'
					}
					steps {
						echo "Running ASAN on Intel"
					}
				}
				stage('Power Build ASAN') {
					steps {
						echo "Skipping ASAN on Power ...."
					}
				}
			} //end parallel
		} //end Build Stage
		stage('DevQA') {
			parallel {
				stage('Intel Basic OPT') {
					agent {
						label 'intel'
					}
					steps {
						echo "Running Basic OPT on Intel"
					}
				}
				//stage('Power Basic OPT') {
				//	agent {
				//		label 'power'
				//	}
				//	steps {
				//		echo "Running Basic OPT on Power"
				//	}
				//}
			} // end parallel
		}
	} //end stages
} //end pipeline













































