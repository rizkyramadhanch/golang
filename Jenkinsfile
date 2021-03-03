pipeline {
    agent any
    // agent {
    //     docker {
    //         image 'damitj07/go-dep-docker-aws'
    //     }
    // }
    environment {
        // VERSION = "${env.BUILD_ID}-${env.GIT_COMMIT}"
        NAME = "golang"
        // IMAGE_REPO = "rizkyramadhanch/golang_cilsy"
        // GIT_URI = "git@bitbucket.org:sample/myapp.git"
        // BRANCH = "${env.BRANCH_NAME}"
        // IMAGE = "${IMAGE_REPO}/${NAME}:${VERSION}"
    }
    stages {
        stage('Build') {
            steps {
                // echo "Running ${VERSION} on ${env.JENKINS_URL}"
                // git branch: "${BRANCH}", credentialsId: 'jenkins-bitbucket-key', url: "${GIT_URI}"
                // echo "for branch ${env.BRANCH_NAME}"
                sh "docker build . -t rizkyramadhanch/golang_cilsy:$BUILD_NUMBER"
                sh "docker push rizkyramadhanch/golang_cilsy:$BUILD_NUMBER"
            }
        }
        // stage('Test') {
        //     steps {
        //         echo 'Skipping Testing..'
        //     }
        // }
        // stage('Artifact') {
        //     steps {
        //         echo 'Deploying.. To Dev'
        //         sh 'aws ecr get-login --no-include-email --region ap-south-1 >> login.sh'
        //         sh 'sh login.sh'
        //         sh "docker push ${IMAGE_REPO}/${NAME}:${VERSION}"
        //     }
        // }
        stage('Deploy') {
            steps {
                sh 'docker pull rizkyramadhanch/golang_cilsy:$BUILD_NUMBER'
                sh 'docker rm -f golang'
                sh 'docker run -dit -p 82:8123 --name ${NAME} rizkyramadhanch/golang_cilsy:$BUILD_NUMBER'
            }
        }
    }
}