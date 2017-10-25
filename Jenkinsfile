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
        docker.withRegistry('http://172.17.0.1:5000', 'nexus') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
      }
}