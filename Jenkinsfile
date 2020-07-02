pipeline {
   agent any

   environment {
            AWS_ACCESS_KEY_ID     = credentials ('AWS_ACCESS_KEY_ID')
            AWS_SECRET_ACCESS_KEY = credentials ('AWS_SECRET_ACCESS_KEY')
        }

   stages {
      stage('scm checkout') {
         steps {
         // Get code from a GitHub repository
	         echo 'retrieving code form scm'
            git 'https://github.com/chine-imo/WAIP2.git'
	         echo 'code retrivial from scm complete'
         }
      }
      // initialize configuration files in working diectory
      stage('initialize tf') {
         steps {
	         echo 'initializing working directory'
            sh 'terraform init'
	         echo 'initialization complete'
         }
      }

      // validates the configuration files in a directory
      stage('validate tf') {
         steps {
	         echo 'validating terraform config files'
            sh 'terraform validate'
	         echo 'validation success'
         }
      }

      // create terraform execution plan
      stage('plan tf') {
         steps {
	         echo 'runnign terraform plan'
            sh 'terraform plan'
	         echo 'planning complete'
         }
      }
      // validates the configuration files in a directory
      stage('apply tf') {
         steps {
	         echo 'applying terraform config to environment' 
            sh 'terraform apply -auto-approve'
	         echo 'deployment complete'
         }
      }      
   }
}
