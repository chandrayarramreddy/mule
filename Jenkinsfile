pipeline
{
		agent any
tools {
  maven 'Maven'
}
		stages
		{
		stage ('Source Code Triggered')
		{
			steps
			{
			checkout([$class: 'GitSCM', branches: [[name: '*']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Sai6696/Test.git']]])
			//properties([pipelineTriggers([pollSCM('* * * * *')])])
            }
		}
		
		stage ('Build Test')
		{	
			steps
			{
			bat 'mvn clean test'
			}
		}
		
		stage ('Deploy')
		{	

			steps
			{
                withCredentials([string(credentialsId: 'Mversion', variable: 'version'), string(credentialsId: 'Musername', variable: 'user'), string(credentialsId: 'Mpassword', variable: 'pass'), string(credentialsId: 'Mdev', variable: 'env1'), string(credentialsId: 'Mprod', variable: 'env2'), string(credentialsId: 'Mqa', variable: 'env3'), string(credentialsId: 'Mbussgrp', variable: 'bg'), string(credentialsId: 'Muri', variable: 'uri'), string(credentialsId: 'Mworktype', variable: 'wt'), string(credentialsId: 'Mworkers', variable: 'wrks')]) {
            bat 'mvn package deploy -Dmuleversion=${version} -Dusername=${user} -Dpassword=${pass} -Denv=${env1} -Dbussgrp=${bg}-Duri=${uri} -Dworktype=${wt} -Dworker=${wrks} -DmuleDeploy'
            }       
			
			}
		}
		
		
		}

}
