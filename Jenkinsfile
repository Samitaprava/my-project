 pipeline{
 tools{
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }
     agent any
	  environment {
        
        NEXUS_CREDENTIALS = 'nexus'
        SSH_CREDENTIALS = 'deploy'
    }
	  stages{
	  
	  stage("checkout"){
	   steps{
	   git'https://github.com/Samitaprava/my-project.git'
	   }
	                  }
	
	   stage("compile"){
	    steps{
		    echo "test"
		 sh 'mvn compile'
		}
		}
		stage("test"){
	    steps{
		 sh 'mvn test'
		}
		}
		stage("package"){
	    steps{
		 sh 'mvn package'
		}
		}
		stage("deploy"){
	    steps{
		 script {
                    sshagent([SSH_CREDENTIALS]) {

                        nexusArtifactUploader artifacts:
			[[artifactId: 'app', classifier: '', file: 'target/myweb.war', type: 'war']], 
			credentialsId: 'nexus', groupId: 'com.idream', 
			nexusUrl: 'http://65.2.4.192:8080/nexus',
			nexusVersion: 'nexus2', protocol: 'http',
			repository: 'http://65.2.4.192:8080/nexus/content/repositories/RepoR/',
			version: '1.6'
		    }
                    }
		}
	    }
	  }
 }
