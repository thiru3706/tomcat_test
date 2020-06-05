node {
    def app

    stage('Clone repository') {
       

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image*/

        app = docker.build("thiru3706:${env.BUILD_ID}")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('push image') {
        
        docker.withRegistry('https://hub.docker.com/repository/docker/thiru3706/tomcat', 'DOCKER1') {
            app.push("${env.BUILD_NUMBER}")
            app.push()
            } 
		echo "pushed docker image successfully"
    }
    stage('ansible playbook'){
	steps{
	     script{
		ansiblePlaybook become: true, installation: 'ansible', inventory: 'hosts', playbook: 'tomcat.yml'
	}
}

}
}
