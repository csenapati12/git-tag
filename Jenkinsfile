pipeline {
  agent any
  properties([parameters([gitParameter(branch: '', branchFilter: '.*', defaultValue: '', description: '', name: 'BRANCH', quickFilterEnabled: false, selectedValue: 'NONE', sortMode: 'NONE', tagFilter: '*', type: 'PT_BRANCH_TAG')])])
  stages {
    stage('Git-para-declarative') {
      steps {
        git branch: "${params.BRANCH}", url: 'https://github.com/csenapati12/git-para-plugin.git'
      }
    }
  }
}
