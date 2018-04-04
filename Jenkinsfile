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
			bat "\"${tool 'MSBuild'}\" \"${WORKSPACE}\\HelloWorld\\HelloWorld.sln\" /p:Configuration=Release /p:Platform=x64 /t:rebuild"
		}

		stage("deploy") {
			zip dir: 'HelloWorld\\\\x64\\\\Release', glob: '*.exe,*.dll', zipFile: 'build.zip'
			emailext attachmentsPattern: 'build.zip', body: '', replyTo: 'No-reply@gmail.com', subject: 'Build is ready', to: 'tucaiyong@gmail.com'
		}
	}
}