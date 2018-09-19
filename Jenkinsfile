node {
    
    try{
        stage('checkout') {
           git 'https://github.com/g0t4/jenkins2-course-spring-boot.git'
        }
        
        def project_path = "spring-boot-samples/spring-boot-sample-atmosphere"
    
        dir(project_path) {
            stage('clean verify') {
              sh '/var/jenkins_home/tools/hudson.tasks.Maven_MavenInstallation/M3/bin/mvn clean verify'
            }
            
            // stage('archive') {
            //   archiveArtifacts 'target/*.jar'
            // }
            
            stage('test jacoco result') {
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'target/site/jacoco/', reportFiles: 'index.html', reportName: 'java code coverage', reportTitles: ''])
                step([$class: 'JUnitResultArchiver', testResults: 'target/surefire-reports/TEST-*.xml'])
            }
        } 
    }catch (err) {
        echo "Caught: ${err}"
    }
}



