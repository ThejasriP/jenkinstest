pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout'
            }
        }
        stage('Build') {
            steps {
                echo 'Clean Build'
                bat 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                bat 'mvn test'
            }
        }
        stage('JaCoCo') {
            steps {
                echo 'Code Coverage'
                jacoco()
            }
        }
       
	    stage('JUnit')
	     {
		     steps{
			       junit '/target/surefire-reports/*.xml'
		     }
	    }
	   stage('Sonar') {
            steps {
//                 echo 'Sonar Scanner'
		    withSonarQubeEnv('SonarQube Server') {
		          bat './gradlew sonarqube'
		    }
	    }
	   }
	    
	    stage('Qwikeye Publisher'){
		    steps{
                      qwikeye 'mahesh'
		    }
	    }
    }
    
    post {
        always {
            echo 'JENKINS PIPELINE'
        }
        success {
            echo 'JENKINS PIPELINE SUCCESSFUL'
        }
        failure {
            echo 'JENKINS PIPELINE FAILED'
        }
        unstable {
            echo 'JENKINS PIPELINE WAS MARKED AS UNSTABLE'
        }
        changed {
            echo 'JENKINS PIPELINE STATUS HAS CHANGED SINCE LAST EXECUTION'
        }
    }
}
