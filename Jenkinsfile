pipeline {
    agent any
         stages{
            stage('SCM Checkout'){
                  steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/csenapati12/git-tag.git']]]) 
                  }
             }
           stage('Read YAML file') {
             steps {
               script{ 
                   datas = readYaml (file: 'repo.yaml') 
                   
                   if(datas.services. hiota_agent.version.toString().startsWith("1.0.") && datas.services.myagent4.version.toString()!="1.0.0")
                    createTag(datas.services.myagent4.repo.toString(),datas.services.myagent4.version.toString())
                   if(datas.services.myagent4.version.toString().startsWith("2.0."))
                    createBranch(datas.services.myagent4.repo.toString(),datas.services.myagent4.version.toString())
                   
                   if(datas.services.myagent1.version.toString().startsWith("1.0.") && datas.services.myagent1.version.toString()!="1.0.0")
                    createTag(datas.services.myagent1.repo.toString(),datas.services.myagent1.version.toString())
                   if(datas.services.myagent1.version.toString().startsWith("2.0.") && datas.services.myagent1.version.toString().startsWith("3.0."))
                    createBranch(datas.services.myagent1.repo.toString(),datas.services.myagent1.version.toString())
                   
                    if(datas.services.myagent2.version.toString().startsWith("1.0.") && datas.services.myagent2.version.toString()!="1.0.0")
                    createTag(datas.services.myagent2.repo.toString(),datas.services.myagent2.version.toString())
                   if(datas.services.myagent2.version.toString().startsWith("2.0."))
                    createBranch(datas.services.myagent2.repo.toString(),datas.services.myagent2.version.toString())
                   
                    if(datas.services.myagent3.version.toString().startsWith("1.0.") && datas.services.myagent3.version.toString()!="1.0.0")
                    createTag(datas.services.myagent3.repo.toString(),datas.services.myagent3.version.toString())
                   if(datas.services.myagent3.version.toString().startsWith("2.0."))
                    createBranch(datas.services.myagent3.repo.toString(),datas.services.myagent3.version.toString())
                   
                   
                }
                  

              }
           }
         }
}

def createBranch(String repo, String version){
   echo "inside createBranch method and repo is "+ repo + " version is "+version               
            
           sh " mkdir Repo "            
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'Repo'], [$class: 'CleanBeforeCheckout']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '6e5c3081-96ac-4a13-9c02-5af7ea7bcabd', url: repo]]])            
            
            sshagent(['6e5c3081-96ac-4a13-9c02-5af7ea7bcabd']) {
              sh " cd Repo && git checkout -b ${version} "
              sh " cd Repo && git push origin ${version} "            
              sh " rm -Rf Repo "
            }
}

def createTag(String repo, String version){           
            sh " mkdir Repo "            
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'Repo'], [$class: 'CleanBeforeCheckout']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '6e5c3081-96ac-4a13-9c02-5af7ea7bcabd', url: repo]]])
            
            sshagent(['6e5c3081-96ac-4a13-9c02-5af7ea7bcabd']) {
                sh " cd Repo && git tag -a ${version} -m '${version}' "
                sh " cd Repo && git push origin ${version} "            
                sh " rm -Rf Repo "
            }  
}
