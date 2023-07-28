//def ReleaseDir = "C:\inetpub\wwwroot\HelloApp"
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
    					    bat "\"${tool 'MSBuild'}\" C:\\D-Drive\\POC\\Jenkins_POC\\Code\\TestApp\\AspDotNetJenkins.sln /p:DeployOnBuild=true /p:DeployDefaultTarget=WebPublish /p:WebPublishMethod=FileSystem /p:SkipInvalidConfigurations=true /t:build /p:Configuration=Release /p:Platform=\"Any CPU\" /p:DeleteExistingFiles=True /p:publishUrl=C:\\D-Drive\\POC\\Jenkins_POC\\build"
    					}
				}
			}
}
