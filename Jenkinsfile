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

		  def slurper = new JsonSlurper()
                  def customer = slurper.parseText(res)

                  println customer.address 

                  println "The json response address object is  "+customer.address.getClass().getName()

                  def addressMap = customer.address
                  id = addressMap.get('id');
                  street = addressMap.get('street');
                  houseNumber = addressMap.get('houseNumber');
                  city = addressMap.get('city');
  
                  println "The response address details are $id ,$city, $street and $houseNumber"
 
                  def accountMap = customer.account
                  id = accountMap.get('id');
                  branch = accountMap.get('branch');
                  acNumber = accountMap.get('acNumber'); 
  
                  println "The response account details are $id ,$branch and $acNumber"
 

                  firstName = customer.get('firstName');
                  lastName = customer.get('lastName');
  
                  println "The response customer details are $firstName and $lastName"

                  println "Done with Get"
		}
            }
        }
    }
}
