pipeline {
    agent {
            label 'docker' 
    }
    environment {
        // list all environmental variables
        VERSION_NO = '1.0'
    }

    parameters {
        string(name: 'VERSION', defaultValue: '1.01', description: 'Version umber')
    }

        stages {
        stage('build-frontend') {
                agent {
                docker {
                    label 'docker' 
                    image 'node:14-alpine'
                    // Run the container on the node specified at the top-level of the Pipeline, in the same workspace, rather than on a new node entirely:
                    reuseNode true
                }
            }
            steps {
                sh 'node --version'
                sh 'cd frontend'
                sh 'npm install'
                sh 'npm run build'
                echo 'Done building frontend'
            }
        }
    //     stage('build-backend') {
    //             agent {
    //             docker {
    //                 label 'docker' 
    //                 image 'node:14-alpine'
    //                 // Run the container on the node specified at the top-level of the Pipeline, in the same workspace, rather than on a new node entirely:
    //                 reuseNode true
    //             }
    //         }
    //         steps {
    //             sh 'node --version'
    //             sh 'cd backend'
    //             sh 'npm install'
    //             sh 'npm run build'
    //             echo 'Done building backend'

    //             // Copy compiled backend for future use in ansible
    //             sh 'cp ./backend/package.json /tmp/workspace/'
    //             sh 'cd backend/dist'
    //             sh 'tar -zcvf /tmp/workspace/backend.tar.gz ./'
    //             echo 'Done COPYING backend'
    //         }
    //     }
    //     stage('test-frontend') {
    //             agent {
    //             docker {
    //                 label 'docker' 
    //                 image 'node:14-alpine'
    //                 // Run the container on the node specified at the top-level of the Pipeline, in the same workspace, rather than on a new node entirely:
    //                 reuseNode true
    //             }
    //         }
    //         steps {
    //             sh 'node --version'
    //             sh 'cd backend'
    //             sh 'npm install'
    //             sh 'npm run build'
    //             sh 'npm run test'
    //             echo 'Done testing frontend'
    //         }
    //     }
    // }
}