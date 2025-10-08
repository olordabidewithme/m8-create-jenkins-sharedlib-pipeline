#!/usr/bin/env groovy

@Library('jenkins-shared-library') _

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
	stage("build Jar") {
		steps {
			script{
				buildJar()
			}
		}
	}        
	stage("build and push image") {
		steps {
			script{
				buildImage 'olordabidewithme/demo-app-3.0'
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
