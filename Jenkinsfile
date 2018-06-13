node("jnlp-slave"){
    def NAME = "webui"
    def HARBOR_URL = "10.202.129.133"
    def HARBOR_PROJECT = "library"
    def IMAGE = "${HARBOR_URL}/${HARBOR_PROJECT}/${NAME}:${BUILD_NUMBER}"

    stage("build"){
        sh "docker build -t ${IMAGE} ."

        withCredentials([[$class: "UsernamePasswordMultiBinding", credentialsId: "harbor", usernameVariable: "USERNAME", passwordVariable: "PASSWORD"]]) {
            sh "docker login --username=${USERNAME} --password=${PASSWORD} ${HARBOR_URL}"
        }

        sh "docker push ${IMAGE}"
    }
}
