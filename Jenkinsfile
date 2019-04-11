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
                   datas = readYaml (file: "${env.YAML}")
                          
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
	   checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/csenapati12/jenkinsfiledemo.git']]])
	   '''
          //  sh "git clone http://chaitanya-Inspiron-5521/csenapati12/gittag.git"
           
}

def createTag(String repo, String version){     
     echo "inside createTag method and repo is "+ repo + " version is "+version  
	//sh "mkdir testrepo"
	sh "cd testrepo"
	checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: repo]]])
        sh "ls"
	sh "git branch -a"
	sh "git branch -a > /var/lib/jenkins/workspace/git-lab-yml-read/branch_version.out"
	sh "chk_result=`grep 6.0.0 /var/lib/jenkins/workspace/git-lab-yml-read/branch_version.out`"
	     sh "echo $chk_result"

	
	//sh "rm -rf testrepo"
     
          
}
