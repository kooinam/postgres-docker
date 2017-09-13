node {
    docker.withRegistry("https://index.docker.io/v1/", '6da4bfc5-12fb-4165-982c-2c2423372ef6') {

        git url: "git@bitbucket.org:hickory_lab/mrn_pg.git", credentialsId: 'b9bcb64d-45fa-47dc-96bf-97f4685f52fa'

        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id

        stage "build"
        def app = docker.build "kooinam/mrn-mongo"

        stage "publish"
        app.push 'latest'
        app.push "${commit_id}"
    }
}