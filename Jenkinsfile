pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
				}
					   }
        stage('Build docker images') {
            when { 
                branch 'master'
				 }
            steps {
			script {
                app=docker.build("devops81/trainschedule")
                app.inside { 
                    sh 'echo $(curl localhost:8080)'
                   }
					}
                
            }
        }
		
		stage('Build docker images') {
            when { 
                branch 'master'
            }
            steps {
			script {
			docker.withRegistry(https://registry.hub.docker.com','docker_hub_login') {
			app.push("${env.Build_Number}")
			
               
            }
        }
    }
}
}
}
