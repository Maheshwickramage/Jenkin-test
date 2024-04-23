pipeline {
agent any
stages {
stage('SCM Checkout') {
steps {
retry(3) {
git branch: 'main', url: 'https://github.com/Maheshwickramage/4278-Jenkins-CI-CDPipeline'
}
}
}
stage('Build Docker Image') {
steps { 
bat 'docker build -t 4278-wickramage/test:%BUILD_NUMBER% .'
}
}
stage('Cleanup Old Container') {
steps {
bat '''
docker rm -f container-test || true
'''
}
}
stage('Run Image') {
steps {
bat '''
docker run -d --name container-test -p 3002:3002 4278-
wickramage/test:%BUILD_NUMBER%
'''
}
}
stage('Verify') {
steps {
bat '''
docker ps
docker logs container-test
'''
}
}
}
}
