#!/usr/bin/env groovy
pipeline {
      agent {
        docker {
            image 'gidraff/rest-image:0.0.1'
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
                sh 'pip install -r tasks/requirements.txt'
            }
        }

        stage("Test") {
            steps {
                sh 'echo "running test"'
                sh 'pip install -r app/requirements.txt'
                sh 'pip install -r tests/requirements.txt'
            }
        }

        stage("Copy Artifacts"){
            steps {
                 archiveArtifacts artifacts:'*,*/,*/*', fingerprint:true
            }
        }
    }
}