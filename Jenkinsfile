node{
    def mavenhome = tool name: "maven3.8.5"
//checkoutstage
stage( 'checkoutcode' ){
git branch: 'development', credentialsId: 'e1575017-54ea-4525-a794-f19b59088253', url: 'https://github.com/mbuk37/maven-web-application.git'
}
//buildstage
stage( 'build' ){
sh "$mavenhome/bin/mvn clean package"
}
//sonarqubereport
stage( 'sonarqube' ){
    sh "$mavenhome/bin/mvn sonar:sonar"
}
//uploading into artifactory repository
stage( 'nexus' ){
    sh "$mavenhome/bin/mvn deploy"
}
//deploy app 
stage ( 'Tomcat' ){
  sshagent(['0aaa74af-72cb-4103-98ea-42da4fd0f821']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.215.138:/opt/apache-tomcat-9.0.59/webapps"
}  
}
}
