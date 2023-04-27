pipeline {

    agent any
    
    environment {
        imagename = "moveho/docker-jenkins-cicd"
        registryCredential = 'docker-credentials'
        dockerImage = ''
    }
    
    stages {
        stage('git clone') {
            steps {
                dir('/home/kevin/cicd') {
                    checkout scmGit(branches: [[name: '*/master']], extensions: [submodule(parentCredentials: true, reference: '', trackingSubmodules: true)], userRemoteConfigs: [[credentialsId: 'MachDnr', url: 'https://github.com/MachDn/docker-jenkins-cicd.git']])
                }
            }
        }
            
         stage('docker-build'){
            steps {
                echo 'Build Docker'
                dir('/home/kevin/cicd'){
                    script {
                        sh "pwd"
                        dockerImage = docker.build imagename
                        
                    }
                }
            }
        }
        
        stage('docker-push'){
            steps{
                echo 'Push Docker'
                script {
                    docker.withRegistry('', registryCredential){
                        dockerImage.push("1.0")
                    }
                }
                
            }
        }
        
    }
}
