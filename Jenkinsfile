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
        docker.withRegistry('http://nexus.local', '') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
      }
}