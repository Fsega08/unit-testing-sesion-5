pipeline {
	agent any
	stages {
		stage ('Build Backend') {
			steps{
				step{
					def mvnHome = tool 'M3'
					sh "${mvnHOME}/bin/mvn mvn clean package -DskipTests=true"
				}
			}		
		}	
	}
}
