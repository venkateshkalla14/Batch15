


pipeline {
    agent any

    stages {
        stage (Checkout) {
            steps {
                 git branch: 'main', url: 'https://github.com/srisaipatel05/gctech.git'
            }
        }
         stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage(dockerfile){
            steps{
                sh 'docker build -t srisaipatel/bunny .'
            }
        }
        stage(login){
            steps{
                sh 'docker login -u srisaipatel -p srisaipatel05'
                sh 'docker push srisaipatel/bunny'
            }
        }
        stage(cont){
            steps{
                sh 'docker rm -f bunny'
                sh 'docker run -d -p 8084:8080 --name bunny srisaipatel/bunny'
            }
        }
    }
}
















































