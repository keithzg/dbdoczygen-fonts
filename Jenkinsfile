#!groovy
pipeline {
    agent { label 'linux && python3 && cmake && fontforge && eot-utils' }
    options { 
		buildDiscarder(logRotator(daysToKeepStr: '240', numToKeepStr: '60', artifactNumToKeepStr: '10')) 
	}
    triggers {
		pollSCM('H/5 * * * *')
	}
	stages {
		stage('Build') {
			steps {
				echo 'Building fonts'
				sh 'cmake . && make'
				archiveArtifacts artifacts: 'oxygen-fonts/Regular-400/Dbdoczygen-Sans.ttf'
				archiveArtifacts artifacts: 'oxygen-fonts/Regular-400/Dbdoczygen-Sans.woff2'
				archiveArtifacts artifacts: 'oxygen-fonts/Regular-400/Dbdoczygen-Sans.eot'
				archiveArtifacts artifacts: 'oxygen-fonts/Bold-700/Dbdoczygen-Sans-Bold.ttf'
				archiveArtifacts artifacts: 'oxygen-fonts/Bold-700/Dbdoczygen-Sans-Bold.woff2'
				archiveArtifacts artifacts: 'oxygen-fonts/Bold-700/Dbdoczygen-Sans-Bold.eot'
				archiveArtifacts artifacts: 'oxygen-fonts/Mono-400/Dbdoczygen-Mono.ttf'
				archiveArtifacts artifacts: 'oxygen-fonts/Mono-400/Dbdoczygen-Mono.woff2'
				archiveArtifacts artifacts: 'oxygen-fonts/Mono-400/Dbdoczygen-Mono.eot'
			}
		}
	}
}

