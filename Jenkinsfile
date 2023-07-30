pipeline {
			agent any
			stages {
				stage('Source'){
					steps{
						checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Gitcredentials', url: 'https://github.com/meetsandip/JenkinsPOC']]])
					}
				}
				stage('Build') {
    					steps {
    					    bat "\"${tool 'MSBuild'}\" C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Test-Pipeline\\TestApp.sln /p:DeployOnBuild=true /p:DeployDefaultTarget=WebPublish -t:restore /p:WebPublishMethod=FileSystem /p:SkipInvalidConfigurations=true /t:build /p:Configuration=Release /p:Platform=\"Any CPU\" /p:DeleteExistingFiles=True /p:publishUrl=C:\\D-Drive\\POC\\Jenkins_POC\\build"
    					}
				}
				stage('Deploy') {
    					steps {
						    bat ("C:\\Windows\\System32\\inetsrv\\appcmd stop apppool /apppool.name:WelcomeSite")
							bat ("C:\\Windows\\System32\\inetsrv\\appcmd stop site /site.name:WelcomeSite")
							bat ("del C:\\D-Drive\\POC\\Jenkins_POC\\build\\Web.config")
    					    bat("xcopy C:\\inetpub\\wwwroot\\WeclomeSite C:\\D-Drive\\POC\\Jenkins_POC\\ApplicationBackup\\backup /O /X /E /H /K")
							bat("xcopy C:\\D-Drive\\POC\\Jenkins_POC\\build C:\\inetpub\\wwwroot\\WeclomeSite /O /X /E /H /K")
							bat ("C:\\Windows\\System32\\inetsrv\\appcmd start apppool /apppool.name:WelcomeSite")
							bat ("C:\\Windows\\System32\\inetsrv\\appcmd start site /site.name:WelcomeSite")
    					}
				}
			}
}
