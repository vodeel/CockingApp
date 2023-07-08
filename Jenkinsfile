pipeline {
 agent any    
 environment{
     token= credentials('docker_token')
     docker_user = credentials('docker_user')
 }
    stages {
        stage('pwd') {
            steps {
                sh 'echo ${token} | docker login -u ${docker_user} --password-stdin'
               
               git branch: 'main', credentialsId: 'vodeel', url: 'https://github.com/vodeel/CockingApp.git'
            }
        }
        
        stage('build') {
            steps {
                sh ' docker build -t vodeel14/httpd:${BUILD_NUMBER} .'
            }
        }
        
        stage('push') {
            steps {
               
                // some block
                sh ' docker push vodeel14/httpd:${BUILD_NUMBER}'
            
            }
        }
    }
    post{
        always{
            sh 'docker logout'
        }
    }
}
