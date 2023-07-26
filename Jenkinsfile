pipeline {
    agent any

    stages {
        stage('Checkout GitHub') {
            steps {
                echo 'Checking out from gitHub'
                //git branch: 'main', credentialsId: '3c6c6d3e-4f17-44ee-a9cc-d06927fd0634', url: 'https://github.com/akashlahane33/PipelineSCM'
            }
        }
        
        stage('Accessing API from external server') {
            steps {
		script {
                  println "The groovy runtime version is $GroovySystem.version"

                  def getURL = new URL('http://localhost:1100/rest-api/customers/1')
                  def connection = getURL.openConnection()
                  connection.requestMethod = 'GET'
                  connection.setRequestProperty("Accept", "application/json");

                  assert connection.responseCode == 200
                  BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));

                  println("\nThe JSON format of customer sent by rest-server...\n");

                  line = reader.readLine();
                  def res =line

                  while (line != null) {
                	println(line);
	
	               line = reader.readLine();
                    }
                  connection.disconnect();
		}
            }
        }
    }
}
