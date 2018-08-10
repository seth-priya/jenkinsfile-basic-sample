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
	      	        steps {
                	    script {
                        	def bStageData = [
                                    "Client JARs": "light",
                                    "Build OPT": "welter",
                                    "Build ASAN": "welter",
                        	]
				def builders = [:]
				for (buildStage in mapToList(bStageData)) {
				    bStage = buildStage[0]
                              	    for (x in archs) {
                                        def arch = x
                                        builders["${arch} ${bStage}"] = {
					    def agentLabel = (arch == "x86_64") ? "${buildStage[1]}weight" : "${buildStage[1]}${arch}"
                                            node(agentLabel) {
						if (bStage == "Build OPT") {
                                                    doBuild(arch, 'OPT')
						} else if (bStage == "Client JARs") {
						    echo "stage = ${bStage}, arch = ${arch}, agentLabel = ${agentLabel}"
						} else if (bStage == "Build ASAN") {
						    echo "stage = ${bStage}, arch = ${arch}, agentLabel = ${agentLabel}"
						}
                                            }
                                        }
				    }
				}
                                parallel builders
                            }
			}
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













































