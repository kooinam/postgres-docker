node {
    docker.withRegistry("${params.DOCKER_REGISTRY_URL}", "${params.DOCKER_REGISTRY_CREDENTIALS}") {

        git url: "${params.GIT_URL}", credentialsId: "${params.GIT_CREDENTIALS}"

        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id

        stage "build"
        def app = docker.build "${params.IMAGE_NAME}"

        stage "publish"
        app.push 'latest'
        app.push "${commit_id}"
    }
}