def app

pipeline {

    agent {
        label 'master'
    }
    
     environment {
     
     	DOCKER_IMAGE_NAME = 'jason2xml'
		DOCKER_IMAGE = 'xml'
     	DOCKER_FILE_DIRECTORY  = '/home/oracle/'
     	DOCKER_CONTAINER_NAME= "container-A"
		CONTAINER_NAME= "container-B"
		DISPLAY='192.168.2.112:1'
		EMAIL_LIST_EXT="${params.MANAGER_EMAIL_ID}"
		PROXY_URL="http://192.168.3.20:3128"
		PROJECT_NAME="DOCKER-PYTHON"
		PROJECT_ENV="TEST"

				
     }
    


    stages {
        
        stage('Cleanup Activity') {
            steps {
             	echo 'cleaning pipeline workspace'
                echo 'cleaning puppet master directory'
               }
           
        }
		
	stage('Build Docker Image') {
            steps {
        		
        		withEnv([]) {
		      	sh '''
						BASEDIR=$(pwd)
																		
						echo "########## Clean Up: Removing existing container A ###########################"
						
						if [ CH\$(docker ps -a -f \"name=\$DOCKER_CONTAINER_NAME\" | grep \$DOCKER_CONTAINER_NAME -o) != "CH" ]; then docker rm -f $DOCKER_CONTAINER_NAME; fi
						if [ CH\$(docker images -q \"$DOCKER_IMAGE_NAME\") != "CH" ]; then docker rmi -f $(docker images -q \"$DOCKER_IMAGE_NAME\"); fi
						sleep 5
						if [ CH\$(docker ps -a -f \"name=\$CONTAINER_NAME\" | grep \$CONTAINER_NAME -o) != "CH" ]; then docker rm -f $CONTAINER_NAME; fi
						docker image prune -f
						if [ CH\$(docker images -q \"$DOCKER_IMAGE\") != "CH" ]; then docker rmi -f $(docker images -q \"$DOCKER_IMAGE\"); fi
						    				
        				
						docker build -t $DOCKER_IMAGE_NAME $BASEDIR/
        				docker run -it -d -v /var/www/:/home/oracle --name=$DOCKER_CONTAINER_NAME  -e DISPLAY=$DISPLAY -e JAVA_HOME=/usr/orps/java/jdk1.8.0_144 $DOCKER_IMAGE_NAME
						docker build -t $DOCKER_IMAGE_NAME $BASEDIR/skeleton/
						docker run -it -d  -v /var/www/:/var/www --name=$CONTAINER_NAME  -e DISPLAY=$DISPLAY -e JAVA_HOME=/usr/orps/java/jdk1.8.0_144 $IMAGE_NAME
					 	
							
		       		'''
				script {
                    if ("${params.PIPELINE_ACTIVITY}".contains("deploy")) {
                        emailext body: "Test has been Completed for Python, Deploy this build in Dev env? recipientProviders: [ [$class: 'RequesterRecipientProvider']], subject: "Test of Jason to xml file has been completed' Pipeline is waiting for input",from:'noreply1@example.net', to: 'vaibhav.parde@example.com'    
                        input message: "Test has Completed, Deploy this in Dev env?", ok: 'Proceed', submitter: 'vaibhav-parde'
                    }
                }	
       		}
       			
        }	
	