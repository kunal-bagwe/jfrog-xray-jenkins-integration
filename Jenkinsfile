pipeline{
    agent any
    stages{
        stage('Jfrog Xray'){
     
     
           steps{
               script{
                sh 'id'
//                 git changelog: false, url: 'https://github.com/kunal-bagwe/docker-example.git'
                 rtServer (
//                    id: "jfrog-cloud", 
                    id: "xray",
                    url: "https://usecase.jfrog.io/artifactory",
   //                 credentialsId: "jfrog-cloud"
                    credentialsId: "xray"
                )
                   /*
                rtDockerPull (
   //                 serverId: 'jfrog-cloud',
                    serverId: 'jenkins-jfrog'
                    image: 'kunalbagwe/consumer:latest',
                    sourceRepo: 'https://hub.docker.com/repository/docker',
                    project: 'xray',
                   buildName: 'docker-builds',
                    buildName: 'test',
                    buildNumber: '6'
                    
                )
                */
                  sh 'docker pull alpine:3.15' 
//                sh 'docker pull kunalbagwe/consumer:latest'
//                sh 'docker tag kunalbagwe/consumer:latest jenkinsxray.jfrog.io/xray-docker-local/consumer:4.0'
               sh 'docker tag alpine:3.15 usecase.jfrog.io/docker-xray/alpine:3.15'   
                   
                rtBuildInfo (
          //          buildName: 'docker-builds',
                       buildName: 'docker-test',
                       buildNumber: '1',
                //       project: 'xray'
                )
                rtPublishBuildInfo (
                    serverId: 'xray',
                   // buildName: 'docker-builds',
                    buildName: 'docker-test',
                    buildNumber: '1',
                //    project: 'xray'
                )
                   
         rtDockerPush(
            serverId: 'xray',
 //          image: "jenkinsxray.jfrog.io/xray-docker-local/consumer:3.0",
            image: 'usecase.jfrog.io/docker-xray/alpine:3.15',
            targetRepo: 'docker-xray',
           // buildName: 'docker-builds',
            buildName: 'docker-test',
//            buildNumber: "${env.BUILD_NUMBER}",
          buildNumber: '1',
        //    project: 'xray'
         )
                   sh 'sleep 50'
                   
                   xrayScan (
                    serverId: 'xray',
                    // If the build is found vulnerable, the job will fail by default. If you do not wish it to fail:
              //      buildName: 'docker-builds',
                      buildName: 'docker-test',
//                    buildNumber: "${env.BUILD_NUMBER}",
                    buildNumber: '1',
                    failBuild: true
           //         project: 'xray'
                   )
                   
                   
                    }
                }
       }
       /*
       stage('Xray Scan'){
           steps{
              rtServer (
//                    id: "jfrog-cloud", 
                    id: "xray",
                    url: "https://usecase.jfrog.io/artifactory",
   //                 credentialsId: "jfrog-cloud"
                    credentialsId: "xray"
                )
              xrayScan (
                    serverId: 'xray',
                    // If the build is found vulnerable, the job will fail by default. If you do not wish it to fail:
              //      buildName: 'docker-builds',
                      buildName: 'docker-test',
//                    buildNumber: "${env.BUILD_NUMBER}",
//                    buildNumber: '1',
                     failBuild: true,
            //         project: 'xray'
                   )
           }
       }
       */
    }  
    }
