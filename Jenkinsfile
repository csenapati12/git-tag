pipeline {
 parameters {
         string(name: 'yaml_value', defaultValue: 'repo.yaml')
  }
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
                  // datas = readYaml (file: 'repo.yaml') 
                  // echo "ymlfile value $yml-file"
                   datas = readYaml (file: "${env.yaml_value}")                    
                             
                   if(datas.services.myagent1.version.toString().endsWith(".0.0"))
                    createBranch(datas.services.myagent1.repo.toString(),datas.services.myagent1.version.toString())
					
                   else
                    createTag(datas.services.myagent1.repo.toString(),datas.services.myagent1.version.toString())
                   
                    if(datas.services.myagent2.version.toString().endsWith(".0.0"))
					createBranch(datas.services.myagent2.repo.toString(),datas.services.myagent2.version.toString())
                    
                   else
				   createTag(datas.services.myagent2.repo.toString(),datas.services.myagent2.version.toString())
                    
                                   
                 }  
              }
           }
         }
}
