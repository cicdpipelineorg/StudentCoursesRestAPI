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
}
node('kubernetes')
{
    stage('deploying to kubernetes')
{
    git 'https://github.com/cicdpipelineorg/StudentCoursesRestAPI.git'
    sh 'envsubst < deploy.yaml | kubectl apply -f -' 
}

}
