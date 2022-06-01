//pipeline as code
//we will intergaret gitmaven in pipeline
pipeline{
    tools{
        jdk 'myjvm'
        maven 'mymaven'
    }
    
    agent any
    stages{
        stage('clone repo')
        {
            steps{
                git 'https://github.com/visheshbathla/maven.git' 
            }
        }
        stage('compile the code')
        {
            steps{
                sh 'mvn compile' 
            }
        }
          stage('test the code')
        {
            steps{
                sh 'mvn test' 
            }
                  post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
                  }
        }
        
              stage('review the code')
        {
            steps{
                sh 'mvn pmd:pmd' 
            }
        }
                      stage(' code coverage')
        {
            steps{
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml' 
            }
             post {
                always {
                    cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: ' **/target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
                }
                  }
            
            
        }
        stage('Package the code')
        {
            steps{
                sh 'mvn package' 
            }
        }
    }

}
