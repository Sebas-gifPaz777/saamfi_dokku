pipeline{
    agent any
    stages{
        stage('Checkout project'){
            steps{
                git branch: 'main', url:'https://github.com/Sebas-gifPaz777/saamfi_dokku.git'
            }
        }
        stage('Project Build'){
            steps{
                sh './mvnw -DskipTest clean package'
            }
        }
        stage('Deploy'){
            steps{
                sshagent(['dokku']){
                    sh 'git remote remove dokku || true'
                    sh 'git remote add dokku dokku@172.23.239.206:saamfi-h2 || true'
                    sh 'GIT_SSH_COMMAND = "ssh -i ~/.ssh/id_rsa StrictHostKeyChecking=no -p 3022" git push dokku main -f '
                }
            }
        }
    }
}