pipeline {
  agent any
  parameters {
    gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
  }
  stages {
    stage('Git-para-declarative') {
      steps {
        git branch: "${params.BRANCH}", url: 'https://github.com/csenapati12/git-para-plugin.git'
      }
    }
  }
}
