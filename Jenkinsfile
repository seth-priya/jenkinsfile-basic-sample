def archs = ["intel", "power"]

def doInit(buildMode) {
	for (x in archs) {
		def arch = x
		def builders = [:]
		builders[arch] = {
		    node(arch) {
			echo "In init BuildMode=${buildMode}, Architecture=${arch}"
		    }
		}
	}
}

pipeline {
	agent none
	stages {
		stage('Init') {
			agent none 
			steps {
				script {
					def builders = doInit("OPT")
			//		for (x in archs) {
			//		    def arch = x
			//		    builders[arch] = {
			//			node(arch) {
			//		    	    doInit("OPT", arch)
			//			}
			//		    }
			//		}
					parallel builders
				}			
			}
		}
		stage('Build') {
			parallel {
				stage('Intel Client JARS') {
					agent {
						label 'intel'
					}
					steps {
						echo "Running Client JARS on Intel"
					}
				}
				stage('Power Client JARS') {
					agent {
						label 'power'
					}
					steps {
						echo "Running Client JARS on Power"
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













































