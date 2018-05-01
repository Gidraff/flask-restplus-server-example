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
                sh 'echo "Installing requirements"'
       
            }
        }

        stage("Test") {
            steps {
                sh 'echo "running tests"'
                sh 'service postgresql start'
                sh 'nosetests --with-coverage'
            }
        }

        stage("Copy Artifacts"){
            steps {
                 archiveArtifacts artifacts:'*,*/,*/*', fingerprint:true
            }
        }
    }
}