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
        app = docker.build("goxplanet/workshop-jenkins")
    }
    stage('Push image') {
        docker.withRegistry('https://registry.cn-hangzhou.aliyuncs.com/goxplanet/workshop-jenkins', 'docker-ali') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
      }
}