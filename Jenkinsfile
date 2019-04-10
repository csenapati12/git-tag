pipeline {
 parameters {
         
	 //string(name: 'myagent1', defaultValue: 'myagent1')
	 choice(name: 'AGENTS', choices: ['myagent1', 'myagent2', 'myagent3'], description: '')
	 choice(name: 'YAML', choices: ['repo.yaml', 'repo1.yaml'], description: '')
	 
  }
    agent any
         stages{
           
           stage('Read YAML file') {
             steps {
               script{ 
                  // datas = readYaml (file: 'repo.yaml') 
                   //echo "ymlfile value $yaml_value"
                   datas = readYaml (file: "${env.yaml_value}")
                          
                   if(datas.services.myagent1.version.toString().endsWith(".0.0"))
                    createBranch(datas.services.myagent1.repo.toString(),datas.services.myagent1.version.toString())
					
                   else
                    createTag(datas.services.myagent1.repo.toString(),datas.services.myagent1.version.toString())
                                                                     
                 }  
              }
           }
         }
}

def createBranch(String repo, String version){
   echo "inside createBranch method and repo is "+ repo + " version is "+version               
            
           sh label: '', script: '''
           mkdir test
	   checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'http://chaitanya-Inspiron-5521/csenapati12/gittag.git']]])
	   '''
          //  sh "git clone http://chaitanya-Inspiron-5521/csenapati12/gittag.git"
           
}

def createTag(String repo, String version){     
     echo "inside createTag method and repo is "+ repo + " version is "+version  
     
          
}
