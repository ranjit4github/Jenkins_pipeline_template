@Library('my-jenkinsfile-library') _

pipeline{
  agent{
    label "win-core"
  }
  environemt{
    appVersion = '1.3.2'
    proj_name = 'myProject'
    dbBuild = "true"
    buildPath = "/src/db/package"
  }
  stages{
    stage('Scan and Build'){
      parallel{
        stage("Scan"){
          agent{
            label "win-core-04"
          }
          stages{
            stage('Sonatype Scan'){
              steps{
                sonatype_scan()
              }
            }
          }
        }
        stage('Build'){
          agent{
            label "win-core-08"
          }
          stages{
            stage('App Build'){
              steps{
                app_build()
              }
            }
            stage('DB Build'){
              steps{
                db_build()
              }
            }
            stage('Publish Artifacts'){
              steps{
                publish_artifacts()
              }
            }
          }
        }
      }
    }
  }
}
