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
				archs = params.engineBuildAndTestArch.split(",")
			}
		}
		stage('Build') {
	      	        steps {
                	    script {
				def subStages = ["Client JARS", "Build OPT"]
				def builders = [:]
				for (s in subStages) {
				    sstage = subStages
                              	    for (x in archs) {
                                        def arch = x
                                        builders["${arch} ${subStages}"] = {
                                      	    def nodeLabel = (arch == "intel") ? "welterweight" : "welter${arch}"
                                            node(nodeLabel) {
                                                doBuild(arch, 'OPT')
                                            }
                                        }
				    }
				}
                                parallel builders
                            }
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













































