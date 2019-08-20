pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat(script: 'C:\\\\Informatica\\\\10.2.2\\\\clients\\\\DeveloperClient\\\\infacmd\\\\infacmd.bat tools deployApplication  -domainName Administrator -username %param_username% -password %param_password% -repositoryService MRS_INFABDM_DEV -od %param_path% -applicationPath %param_folder_name%/%param_application_name%', label: 'Export the IRA File', returnStatus: true)
      }
    }
    stage('Removing existing version') {
      steps {
        bat(label: 'Stop existing version of the application', script: 'C:\\\\Informatica\\\\10.2.2\\\\clients\\\\DeveloperClient\\\\infacmd\\\\infacmd.bat dis stopApplication -domainName Administrator -username %param_username% -password %param_password% -serviceName DIS_INFABDM_DEV  -application %param_target_application_name% || true')
        bat(script: 'C:\\\\Informatica\\\\10.2.2\\\\clients\\\\DeveloperClient\\\\infacmd\\\\infacmd.bat dis undeployApplication -domainName Administrator -username %param_username% -password %param_password% -serviceName DIS_INFABDM_DEV  -application %param_target_application_name% || true', label: 'Undeploy existing version of the application')
      }
    }
    stage('Deploying') {
      steps {
        bat(script: 'C:\\\\Informatica\\\\10.2.2\\\\clients\\\\DeveloperClient\\\\infacmd\\\\infacmd.bat dis deployApplication -domainName Administrator -username %param_username% -password %param_password% -serviceName DIS_INFABDM_DEV -FileName %param_path%\\\\%param_application_name%.iar -application %param_target_application_name%', label: 'Deploying the new version of the application', returnStatus: true)
      }
    }
  }
}