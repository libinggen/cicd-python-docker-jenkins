node {
    def application = "pythonapp"
    def dockerhubaccountid = "libinggenjp"
    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
    }

    stage('Push image') {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
            app.push()
            app.push("latest")
        }
    }

    stage('Deploy') {
        sh ("docker ps -q --filter \"name=${application}\" | grep -q . && docker stop ${application} && docker rm ${application} || true")
        
        sh ("docker run --name ${application} -d -p 3333:3333 ${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
    }

    stage('Remove old images') {
        // remove old docker images
        sh("docker rmi ${dockerhubaccountid}/${application}:latest -f")
    }
}
