node 
{
    def mavenHome=tool name: "maven-3.9.9"
    stage('git checkout')
    {
        git credentialsId: '523ecfec-afa0-40e9-8817-b649dc2f6aa4', url: 'https://github.com/anthatianithagoud/final.git'
    }
    stage('maven build')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
     stage('nexus deploy')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
     stage('Deploy to Tomcat') {
        echo "Deploying WAR file using curl..."

        sh """
            curl -u admin:admin \
            --upload-file /var/lib/jenkins/workspace/scripted-pl/target/maven-web-application.war \
            "http://3.82.36.120:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """
    }
}//node closing
