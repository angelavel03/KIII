node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
        app = docker.build("angelavel03/kiii-jenkins")
    }
    stage('Push image') {   
        def safeTag = env.BRANCH_NAME.replaceAll('/', '-').toLowerCase()
        docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
            app.push("${safeTag}-${env.BUILD_NUMBER}")
            app.push("${safeTag}-latest")
        }
    }
}
