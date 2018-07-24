#!groovy
pipeline {
    agent { label 'linux && python3 && cmake && fontforge && eot-utils' }
    options { 
		buildDiscarder(logRotator(daysToKeepStr: '240', numToKeepStr: '60', artifactNumToKeepStr: '50')) 
	}
    triggers {
		pollSCM('H/5 * * * *')
	}
	stages {
		stage('Build') {
			steps {
				echo 'Building xlsx2csv'
				sh 'cmake . && make'
				archiveArtifacts artifacts: 'oxygen-fonts/mono-400/OxygenMono-Regular.ttf'
				archiveArtifacts artifacts: 'oxygen-fonts/Bold-700/Oxygen-GMCL-Sans-Bold.ttf'
				archiveArtifacts artifacts: 'oxygen-fonts/Regular-400/Oxygen-GMCL-Sans.ttf'
			}
		}
	}
}

