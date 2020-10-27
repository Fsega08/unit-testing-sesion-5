pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            
            environment {
                mvnHOME = tool 'MAVEN_HOME'
            }

            steps {

				sh  "${mvnHOME}/bin/mvn clean package -DskipTests=true"	
            }
        }
        
        stage ('Run test') {
            
            environment {
                mvnHOME = tool 'MAVEN_HOME'
            }

            steps {

				sh  "${mvnHOME}/bin/mvn test"	
            }
        }
        
        stage ('Sonar Analysts') {
            
            environment {
                scanHOME = tool 'SONAR_SCANNER'
            }

            steps {
				withSonarQubeEnv('SONAR_LOCAL'){
					sh  "${scanHOME}/bin/sonar-scanner -e -Dsonar.projectKey=backend -Dsonar.host.url=http://sonarqube:9000 -Dsonar.login=15c98633513271136de471bed3ab5c415e0975cd -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/src/test/**,**/entity/**"
				}
            }
        }

        stage ('Quality Gate') {

            steps {

            	sleep(5)
            	timeout(time: 3,unit: 'MINUTES'){
					waitForQualityGate abortPipeline:true
				}
            }
        }
    }
 
    post {
    	always{
			junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'	
		}
	}
}