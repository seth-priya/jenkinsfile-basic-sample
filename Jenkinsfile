def doInit(buildMode, arch) {
	echo "In init BuildMode=${buildMode}, Architecture=${arch}"
}

def archs = ["intel", "power"]
def builders = [:]
pipeline {
	agent none
	stages {
		stage('Init') {
			agent none 
			steps {
				script {
					for (int i=0; i < archs.size(); i++) {
					    builders[${archs[i]}] = {
						node(${archs[i]}) {
					    	    doInit("OPT", ${archs[i]})
						}
					    }
					}
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













































