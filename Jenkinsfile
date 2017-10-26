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
            docker-compose --host 118.178.240.29 up --force-recreate -d
        '''
    }
}