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
			sh 'docker build .'
                
            }
        }
		

}
	stage('Push docker images') {
            when { 
                branch 'master'
            }
			docker.withRegistry('https://registry.hub.docker.com','dockercred') {
			app.push("${env.Build_Number}")

			app.push("latest")

            }

}
}
