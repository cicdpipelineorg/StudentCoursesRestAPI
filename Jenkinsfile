def registry = "sujith140/jenkins:$BUILD_NUMBER"
def registryCredential = 'dockerhubfinal'
def dockerImage = ''
node('docker')
{
stage('git')
{
git 'https://github.com/cicdpipelineorg/StudentCoursesRestAPI.git'
}
stage('building image')
{

dockerImage = docker.build registry
}

stage('push image to repository')
{
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
stage('cleaning up')
{
sh "docker rmi $registry"
}
stage('deploying to kubernetes')
{
    sh label: 'kubernetes', script: 'git clone https://github.com/cicdpipelineorg/StudentCoursesRestAPI.git && cd StudentCoursesRestAPI'
    sh label: 'kubernetes', script: 'envsubst < deploy.yaml | kubectl apply -f -' 
}

}
