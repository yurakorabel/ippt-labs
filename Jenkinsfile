pipeline {
    agent { label 'RedHatSlave' }
    stages {
        stage('Docker version') {
            steps {
                sh '''
                    echo $USER
                    docker version
                '''
            }
        }
        stage('Build docker image') {
            steps {
                sh '''
                    docker build -t yurakorabel/ippt-lab:latest .
                '''
            }
        }
        stage('Push docker image to DockerHub') {
            steps{
                withDockerRegistry(credentialsId: 'DockerHub', url: 'https://index.docker.io/v1/') {
                    sh '''
                        docker push yurakorabel/ippt-lab:latest
                    '''
                }
            }
        }
        stage('Docker delete local image') {
            steps {
                sh '''
                    docker rmi yurakorabel/ippt-lab:latest
                '''
            }
        }
    }
}
