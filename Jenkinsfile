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

    }
}