pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/ashwinr200/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t ashwinr2001/ashwinphpprojectmay042025:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push ashwinr2001/ashwinphpprojectmay042025:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 2023:80 ashwinr2001/ashwinphpprojectmay042025:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 akshu20791/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.4.38 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.4.38 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
