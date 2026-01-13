pipeline
{
  agent any
  stages{
    stage('checkout')
    {
      steps
      {
        echo 'fetching source code'
        checkout scm
      }
    }
    stage('Code quality check!')
    {
      steps
      {
        echo 'checking code quality'
        bat '''
        findstr GOOD quality.txt > nul
        if errorlevel 1(
        echo Code Quality Failed
        exit 1
        )
        else
        (
         echo Code Quality Passed
        )'''
        
      }
    }
    stage('Generate Report')
    {
      steps
      {
        echo 'Generating build Report'
        bat '''
        mkdir reports
        echo Build Successful>reports\\build-report.txt
        '''
      }
    }
    stage('Archive Artifacts')
    {
      steps{
        echo 'Archiving reports'
        archiveArtifacts artifacts:'reports/*.txt',fingerprint:true
      }
    }
  }
  post
  {
    success{
      echo 'Ppiline completed sucessfully'
    }
    failure
    {
      echo 'pipline failed code blocked'
    }
  }
}
