pipeline {
	agent {
		label 'master'
    }
    environment {
		MAJOR_VERSION = 1
    }
    stages {
        stage('deploy') {
            agent {
                label 'master'
            }
            steps {
                sh "echo Branch: ${env.BRANCH_NAME}"
                sh "pwd"
                sh "ls -al"
                sh "ansible-playbook -i inventory playbook.yml -e @extravar.yml"
            }
        }


    }
    post {
    	failure {
        	emailext(
        	  subject: "${env.JOB_NAME} [env.${BUILD_NUMBER}] Failed!",
        	  body: "check ${env.JOB_NAME} [env.${BUILD_NUMBER}]",
              to: "wangnan.alvin@gmail.com"
        )
      } 

    	success {
        	emailext(
        	  subject: "${env.JOB_NAME} [env.${BUILD_NUMBER}] Succeeded!",
        	  body: "check ${env.JOB_NAME} [env.${BUILD_NUMBER}]",
              to: "wangnan.alvin@gmail.com"
        )
      } 
    } 
}

