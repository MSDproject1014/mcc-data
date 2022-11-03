node {
    stage ("Checkout DataApi") {
        git branch: 'main', url: 'https://github.com/MSDproject1014/mcc-data.git'
    }
    
    stage ("Gradle Build - DataApi") {
        sh 'gradle clean build'
    }
    
    stage ("Gradle Bootjar-Package - DataApi") {
        sh 'gradle bootjar'
    }
    
    stage ("Containerize the app-docker build - DataApi") {
        sh 'docker build --rm -t mccdata:v1.0 .'
    }
    
    stage ("Inspect the docker image - DataApi"){
        sh "docker images mccdata:v1.0"
        sh "docker inspect mccdata:v1.0"
    }
    
    stage ("Run Docker container instance - DataApi"){
        sh "docker run -d --rm --name mccdata -p 8080:8080 mccdata:v1.0"
     }
    
    stage('User Acceptance Test - DataApi') {
	
	  def response= input message: 'Is this build good to go?',
	   parameters: [choice(choices: 'Yes\nNo', 
	   description: '', name: 'Pass')]
	
        if(response=="Yes") {
            stage('Deploy to Kubenetes cluster - DataApi') {
                sh "kubectl create deployment mccdata --image=mccdata:v1.0"
                sh "kubectl expose deployment mccdata --type=LoadBalancer --port=8080"
            }
	    }
    }

    stage("Production Deployment View"){
        sh "kubectl get deployments"
        sh "kubectl get pods"
        sh "kubectl get services"
    }
}
