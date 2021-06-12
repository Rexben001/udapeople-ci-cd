pipeline {
    agent any
    environment {
        // list all environmental variables
        VERSION_NO = '1.0'
        // credentials('test-cred') finds the credential name from Jenkins
        SECRETS = credentials('test-cred')
    }

    tools {
        // Jankins supports 3 build tools, maven, jdk and gradle 
        maven "Maven"
    }

    parameters {
        string(name: 'VERSION', defaultValue: '1.01', description: 'Version umber')
        choice(name: 'VERSION_TAGS', choices: ['js', 'ts', 'cs', 'ns'], description: 'version tags array')
        booleanParam(name: 'BUILDS', defaultValue: true, description: 'Builds feedback')
    }

        stages {
        stage('build-frontend') {
                agent {
                docker {
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
        stage('build-backend') {
                agent {
                docker {
                    image 'node:14-alpine'
                    // Run the container on the node specified at the top-level of the Pipeline, in the same workspace, rather than on a new node entirely:
                    reuseNode true
                }
            }
            steps {
                sh 'node --version'
                sh 'cd backend'
                sh 'npm install'
                sh 'npm run build'
                echo 'Done building backend'

                // Copy compiled backend for future use in ansible
                sh 'cp ./backend/package.json /tmp/workspace/'
                sh 'cd backend/dist'
                sh 'tar -zcvf /tmp/workspace/backend.tar.gz ./'
                echo 'Done COPYING backend'
            }
        }
        stage('test-frontend') {
                agent {
                docker {
                    image 'node:14-alpine'
                    // Run the container on the node specified at the top-level of the Pipeline, in the same workspace, rather than on a new node entirely:
                    reuseNode true
                }
            }
            steps {
                sh 'node --version'
                sh 'cd backend'
                sh 'npm install'
                sh 'npm run build'
                sh 'npm run test'
                echo 'Done testing frontend'
            }
        }
    }
}