node {
    stage ("Checkout DataService"){
        git branch: 'main', url: 'https://github.com/foxwas/sept26-bah-mcc-data.git'
    }
    
    stage ("Gradle Build - DataService") {
	
        sh 'gradle clean build'

    }
    
    stage ("Gradle BootJar-Package - DataService") {
        sh 'gradle bootJar'
    }
    
    stage('User Acceptance Test - DataService') {
	
	  def response= input message: 'Is this build good to go?',
	   parameters: [choice(choices: 'Yes\nNo', 
	   description: '', name: 'Pass')]
	
	  if(response=="Yes") {

	    stage('Release- DataService') {
	     sh 'gradle build -x test'
	     sh 'echo DataService is ready to release!'

	    }
	  }
    }
}
