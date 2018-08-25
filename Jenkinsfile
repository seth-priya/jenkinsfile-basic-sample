import org.jenkinsci.plugins.pipeline.modeldefinition.Utils

def call(boolean condition, body) {
    def config = [:]
    body.resolveStrategy = Closure.OWNER_FIRST
    body.delegate = config

    if (condition) {
        body()
    } else {
        Utils.markStageSkippedForConditional(STAGE_NAME)
    }
}

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

def archs = []

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
				echo "Init"
				script { archs = params.engineBuildAndTestArch.split(",") }
			}
		}
		stage('Build') {
			parallel {
				stage('Client JARS') {
					agent {
						label 'intel'
					}
					steps {
						echo "Running Client JARS on Intel"
					}
				}			
				stage('Build OPT') {
					agent {
						label 'intel'
					}
					steps {
						echo "Running Build OPT on Intel"
					}
				}
				stage('Build ASAN') {
					agent {
						label 'intel'
					}
					steps {
						echo "Running ASAN on Intel"
					}
				}
				stage('Build Power') {
				agent none
				steps {
                		    script {
                        		def bStageData = [
                                    		"Build OPT": ["welter", "0"],
                        		]
					def builders = [:]
					def buildStages = bStageData.keySet()
					for (buildStage in buildStages) {
				    		def bStage = buildStage                              	    
                                        	builders["${bStage} Power"] = {
					    		def agentLabelPrefix = bStageData[bStage][0]
					    		def agentLabel = "${agentLabelPrefix}power"
                                            		node(agentLabel) { 
								if (bStage == "Build OPT") {
                                                    			doBuild('ppc64le', 'OPT')
								}
							} // end node
                                            	} // end builders
					} // end for build stages
                                 
				   
                                    parallel builders
				    } // end script
				} //end steps
				} // end stage Power									
			} // end parallel
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













































