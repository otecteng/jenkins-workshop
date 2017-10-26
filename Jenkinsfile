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
        app = docker.build("demo/app")
    }
    stage('Push image') {
        docker.withRegistry('http://118.178.240.29:5000', 'nexus') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
      }
}