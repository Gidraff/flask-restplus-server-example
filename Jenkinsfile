#!/usr/bin/env groovy
pipeline {
      agent {
        docker {
            image 'gidraff/rest-image:0.0.2'
            args '-u root:root'
        }
      }

    stages {
       
        stage("Build") {
            steps {
                sh 'echo "checking out scm"'
                checkout scm
                sh 'echo "Install projects dependencies"'
                sh 'pip install --upgrade pip'
                sh 'ls'
                sh 'pip install -r tasks/requirements.txt'
            }
        }

        stage("Test") {
            steps {
                sh 'echo "running test"'
                sh 'echo "teststststsct"'
                sh 'pip install -r app/requirements.txt'
                sh 'pip install -r tests/requirements.txt'
                sh 'export FLASK_CONFIG=testing'
                sh 'py.test'
            }
        }

        stage("Copy Artifacts"){
            steps {
                sh 'echo "copying artifacts"'
                 archiveArtifacts artifacts:'*,*/,*/*', fingerprint:true
            }
        }
    }
}