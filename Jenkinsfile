#!/user/bin/env groovy

retriever: modernSCM(
    [$class: 'GitSCMSource',
    remote: 'https://github.com/olordabidewithme/m8-jenkins-shared-library.git',
    credentials: 'git-credentials']
)

def gv

pipeline {   
    agent any
    tools {
        maven 'maven-3.9.2'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }        
	stage("build and push image") {
		steps {
			script{
				buildJar 'olordabidewithme/demo-app-3.0'
				dockerLogin()
				dockerPush 'olordabidewithme/demo-app-3.0'
			}
		}
	}
        stage("deploy") {
        	steps {
                	script {
                    		gv.deployApp()
                	}	
            	}
        }               
    }
} 
