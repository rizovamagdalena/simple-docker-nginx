node {
    def app

    stage('Clone repository') {
        git url: 'https://github.com/rizovamagdalena/simple-docker-nginx.git', branch: 'main'
    }

    stage('Build image') {
        app = docker.build("rizovamagdalena/nginx-test:latest")
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("latest")
        }
    }
}