node() {
	if (!isUnix()) {
		stage("Prepare") {
			checkout(
			[$class: 'GitSCM', 
			branches: [[name: '*/master']], 
			doGenerateSubmoduleConfigurations: false, 
			extensions: [], 
			submoduleCfg: [], 
			userRemoteConfigs: [[
				credentialsId: 'ec012787-6d02-4135-a1be-7b7d1b70aa01', 
				url: 'https://github.com/tucaiyong/JenkinsTest.git'
				]]
			])
		}

		stage("build") {
			bat "MsBuild.exe '${WORKSPACE}\\HelloWorld\\HelloWorld.sln' /p:Configuration=Release /p:Platform=x64 /t:rebuild"
		}

		stage("deploy") {
			zip dir: '${WORKSPACE}\\\\HelloWorld\\\\x64\\\\Release', glob: '<patternset><include name="*.exe"/><include name="*.dll"/></patternset>', zipFile: '${WORKSPACE}\\\\build.zip'
			emailext attachmentsPattern: 'build.zip', body: '', replyTo: 'No-reply@gmail.com', subject: 'Build is ready', to: 'tucaiyong@gmail.com'
		}
	}
}