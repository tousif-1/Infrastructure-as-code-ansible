pipeline {
	agent {
		label 'master'
    }
    environment {
		MAJOR_VERSION = 1
    }
    stages {
        stage('deploy-test') {
            agent {
                label 'master'
            }
            when {
                branch 'development'
            }
            steps {
                sh "echo Branch: ${env.BRANCH_NAME}"
                sh "ansible-playbook -i inventory playbook.yml -e @testvar.yml -vvv"
            }
        }

        stage('deploy-prod') {
            agent {
                label 'master'
            }
            when {
                branch 'master'
            }
            steps {
                sh "echo Branch: ${env.BRANCH_NAME}"
                sh "ansible-playbook -i inventory playbook.yml -e @prodvar.yml"
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

