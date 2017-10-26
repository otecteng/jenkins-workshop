node {
    def app

    stage('Clone repository') {
        checkout scm
    }
    stage('compile jar') {
        sh '''
            ./gradlew build
        '''
    }
    input 'build image?'
    stage('Build image') {
        app = docker.build("demo/app")
    }
    input 'push?'
    stage('Push image') {
        docker.withRegistry('http://118.178.240.29:5000', 'nexus') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
    input 'deploy to qa?'
    stage('deploy') {
        sh '''
            DOCKER_HOST="tcp://118.178.240.29:2375" docker-compose up --force-recreate -d
        '''
    }
}