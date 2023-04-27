node {   
    stage('Clone repository') {
        git credentialsId: 'git', url: https://github.com/MachDn/docker-jenkins-cicd.git'
    }
    
    stage('Build image') {
       dockerImage = docker.build("moveho/docker-jenkins-cicd:latest")
    }
    
 stage('Push image') {
        withDockerRegistry([ credentialsId: "docker-credentials", url: "" ]) {
        dockerImage.push()
        }
    }    
}
