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
        sh ("docker ps -a --format '{{.Names}}' | grep ${dockerhubaccountid}/${application} | xargs -r docker stop || true")
        sh ("docker ps -a --format '{{.Names}}' | grep ${dockerhubaccountid}/${application} | xargs -r docker rm || true")
        
        sh ("docker run --name ${dockerhubaccountid}/${application} -d -p 3333:3333 ${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
    }

    stage('Remove old images') {
        // remove old docker images
        sh("docker rmi ${dockerhubaccountid}/${application}:latest -f")
    }
}
