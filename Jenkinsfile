#!/usr/bin/env groovy
pipeline {
     agent any
     stages {
       stage('Get crendentials') {
         steps {
          script {
              withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId:'artifactory_user', usernameVariable: 'ARTIFACTORY_USER', passwordVariable: 'ARTIFACTORY_TOKEN']]) {
                  env.JK_CAI_ARTIFACTORY_TOKEN = env.ARTIFACTORY_TOKEN
                  env.JK_CAI_ARTIFACTORY_USER = env.ARTIFACTORY_USER
              }
          }
         }
       }

      stage('init Container') {
          agent {
              withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId:'artifactory_user', usernameVariable: 'ARTIFACTORY_USER', passwordVariable: 'ARTIFACTORY_TOKEN']]) {              
            dockerfile {
              additionalBuildArgs "--build-arg CAI_ARTIFACTORY_TOKEN=${ARTIFACTORY_TOKEN}"
              label 'master'
            }
              }
          }
          steps {
              sh "echo ${env.JK_CAI_ARTIFACTORY_USER}"
          }
      }
     }
}
