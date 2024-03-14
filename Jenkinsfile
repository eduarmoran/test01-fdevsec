pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }

    stages {
        stage('test01 FortiDevSec') {
            steps {
                echo 'Hello World'
            }
        }
        
    
    stage('Build') { 
            steps { 
                script{
                 /*sh 'docker build -t test01 .'*/
                 app = docker.build("test01-fdevsec")
                }
            }
        }
      
       
    stage('SAST FortiDevSec'){
            steps {
                 sh 'env | grep -E "JENKINS_HOME|BUILD_ID|GIT_BRANCH|GIT_COMMIT" > /tmp/env'
                 sh 'docker pull registry.fortidevsec.forticloud.com/fdevsec_sast:latest'
                 sh 'docker run --rm --env-file /tmp/env --mount type=bind,source=$PWD,target=/scan registry.fortidevsec.forticloud.com/fdevsec_sast:latest'
            }
        }
             
    /*
    stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://363412468025.dkr.ecr.us-east-2.amazonaws.com/test01-fdevsec', 'ecr:us-east-2:emoran') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
        
    stage('Deploy'){
            steps {
                 sh 'kubectl apply -f deployment.yml'
            }
        }             
        
    stage('DAST FortiDevSec'){
            steps {
                 sh 'sleep 1m'
                 sh 'env | grep -E "JENKINS_HOME|BUILD_ID|GIT_BRANCH|GIT_COMMIT" > /tmp/env'
                 sh 'docker pull registry.fortidevsec.forticloud.com/fdevsec_dast:latest'
                 sh 'docker run --rm --env-file /tmp/env --mount type=bind,source=$PWD,target=/scan registry.fortidevsec.forticloud.com/fdevsec_dast:latest'                 
            }
        }
       */ 
    }
}
