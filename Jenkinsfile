node {
    def application = "pythonapp"
    def dockerhubaccountid = "libinggen"
    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        steps {
            script {
                withEnv(["PATH+DOCKER=/usr/local/bin"]) {
                    sh 'docker build -t libinggen/pythonapp:3 .'
                }
            }
        }
    }

    stage('Push image') {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
        app.push()
        app.push("latest")
    }
    }

    stage('Deploy') {
        sh ("docker run -d -p 3333:3333 ${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
    }

    stage('Remove old images') {
        // remove old docker images
        sh("docker rmi ${dockerhubaccountid}/${application}:latest -f")
   }
}
