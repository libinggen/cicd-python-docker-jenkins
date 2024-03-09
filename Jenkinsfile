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
        sh ("docker ps -a --format '{{.Names}}' | grep ${application} | xargs -r docker stop || true")
        sh ("docker ps -a --format '{{.Names}}' | grep ${application} | xargs -r docker rm || true")

        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
            app.push()
            app.push("latest")
        }
    }

    stage('Deploy') {
        sh ("docker run --name ${application} -d -p 3333:3333 ${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
    }

    stage('Remove old images') {
        // remove old docker images
        sh("docker rmi ${dockerhubaccountid}/${application}:latest -f")
    }
}
