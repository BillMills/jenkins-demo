pipeline {    

    agent any    
    
    environment {
        DOCKER_TLS_VERIFY='1'                                                                                               
        COMPOSE_TLS_VERSION='TLSv1_2'                                                                                       
        DOCKER_CERT_PATH='/home/jenkins/admincerts'                                                                       
        DOCKER_HOST='tcp://ec2-34-201-11-216.compute-1.amazonaws.com:443'
        DTR_FQDN_PORT='ec2-34-201-11-216.compute-1.amazonaws.com:4443'
    }

    stages {
        stage('Build') {
            environment {
                DTR_ACCESS_KEY = credentials('jenkins-dtr-access-token')
            }
            steps {
                sh 'echo ${DTR_FQDN_PORT} ; \
                    docker image build -t ${DTR_FQDN_PORT}/engineering/jenkins-demo:build-${BUILD_ID} . ; \
                    docker login -u jenkins -p ${DTR_ACCESS_KEY} ${DTR_FQDN_PORT} ; \
                    docker image push ${DTR_FQDN_PORT}/engineering/jenkins-demo:build-${BUILD_ID}'
            }
        }
    }
}
