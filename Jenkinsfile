pipeline {
    agent any
    parameters {
        string(name: 'TomcatURL', defaultValue: 'http://3.87.56.145:8080/', description: 'What is the tomcat IP?')
        string(name: 'contextpath', defaultValue: 'sampleapp-dev', description: 'What is the context pat?')
    }
    tools {

        maven "maven"
    }

    stages {
        stage('SCM-checckout') {
            steps {

                git 'https://github.com/VamsiGullapalli/SampleWebApplication.git'
                
            }
        }
        stage('Maven-Build') {
            steps {
                
                sh "mvn -v"
                sh "mvn clean package"
            }
        }  
        stage('test-cases') {
            steps {
                echo 'testing'
            }
        }
        stage('deploy') {
            steps {
                echo "deploying to Tomcat URL"
                echo "${params.TomcatURL}"
                echo "${params.contextpath}"
                deploy adapters: [tomcat9(credentialsId: 'tomcat-deploy', path: '', url: "${params.TomcatURL}")], contextPath: "${params.contextpath}", onFailure: false, war: '**/*.war'
                echo 'URL to access application is' 
                echo "${params.TomcatURL}/${params.contextpath}"
            }
        }               
    }
}

