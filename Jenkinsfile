node {
	checkout scm
	env.PATH = "${tool 'Maven3'}/bin:${env.PATH}"
	stage('Package'){
	 dir('webapp'){
	  sh 'mvn clean package -DskipTests'
	 }
	}

	stage('Create Docker Image') {
	 dir('webapp') {
	  docker.build("pduong/sample-maven-project:${env.BUILD_NUMBER}")
	 }
	}
	
	
	stage ('Run Application') {
	 try {
	  sh "docker run pduong/sample-maven-project:${env.BUILD_NUMBER}"
	 } catch (error) {
	 } finally {
	    echo "DONE"
	 }
	}

	stage('Run Tests and Publish to Docker Hub') {
	 try {
	  dir('webapp') {
	     sh "mvn test"
	      docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
           	 docker.build("pduong/sample-maven-project:${env.BUILD_NUMBER}").push("${env.BUILD_NUMBER}")
              }
	  }
	 } catch(error) {
	 
	 } finally {
	    
	 }
	}
}
