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
    stage('Build image') {
        app = docker.build("172.17.0.1:5000/app")
    }
    stage('Push image') {
        docker.withRegistry('http://nexus.local', '') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
      }
}