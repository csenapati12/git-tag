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

}

def createTag(String repo, String version){
    def repoTag=repo
    echo "inside createTag method and repo is "+ repoTag + " version is "+version
    echo "!!!!!!!!!!!!!!!!!! Cloning Code !!!!!!!!!!!!!!!!!!!! "+ repoTag
    
    
    //checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: repo]]])
    //checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/csenapati12/ansible-playbook.git']]])
  
  
  checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: repo]]])
  
  
    sh """
     git checkout master
     git branch
     git config --global user.name "csenapati12"
                             git config --global user.email csenapati12@gmail.com
     git tag -a ${version} -m '${version}' 
  #   git remote add origin $repo
     git remote -v
     git push --set-upstream origin ${version}
     
  """
  
}
