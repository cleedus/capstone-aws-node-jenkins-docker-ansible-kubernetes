node {
def registry = 'cleedus/cloudops'
def customImage = ''
def registryCredential = 'dockerhub'
stage('Checkout Repo'){

    checkout scm
}
stage('Build DockerFile'){

    customImage = docker.build("${registry}:${env.BUILD_ID}")
}
stage('Linting JavaScript'){
customImage.inside{
    sh 'eslint "**/*.js"'
}
}
stage('Upload image to dockerhub'){
    docker.withRegistry('', registryCredential){
    customImage.push('blue')
}
}
stage('Deploy App'){
    
    sh 'ansible-playbook ./playbooks/deployment-play.yml'
    sh 'ansible-playbook ./playbooks/service-play.yml'
}
}

