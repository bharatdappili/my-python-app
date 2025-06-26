pipeline {
    agent any

    environment {
        ARTIFACTORY_SERVER = 'artifactory'  // Set in Jenkins > Configure System
        ARTIFACTORY_REPO = 'my-python-generic'      // Must exist in JFrog
    }

    stages {

        stage('Build Python Package') {
            steps {
                sh 'python3 setup.py sdist'
            }
        }

        stage('Upload to JFrog Artifactory') {
            steps {
                script {
                    def server = Artifactory.server(ARTIFACTORY_SERVER)

                    def uploadSpec = """{
                        "files": [{
                            "pattern": "dist/*.tar.gz",
                            "target": "${ARTIFACTORY_REPO}/my-python-app/"
                        }]
                    }"""

                    server.upload(spec: uploadSpec)
                }
            }
        }
    }
}
