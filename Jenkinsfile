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
        
          stage('Ansible Init') {
            steps {
                script {
                
               def tfHome = tool name: 'Ansible'
                env.PATH = "${tfHome}:${env.PATH}"
                 sh 'ansible --version'
                    
            }
            }
        }
        
        
        
        stage('Ansible Deploy') {
             
            steps {
                 
              dir('dev/ansible')
              {
 
    stage('ansible playbook'){
	steps{
	     script{
		ansiblePlaybook become: true, installation: 'ansible', inventory: 'hosts', playbook: 'tomcat.yml'
	}
}

}
}
