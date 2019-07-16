/**
  Workfow to download and execute a SSL Test connexion
  @author kuisatahverat
 **/
env.targetHost = targetHost
node () {
  stage ('Env'){
    if (isUnix()) {
      sh 'export'
    }

  }
  stage ('Download sources'){
    tool name: 'Default', type: 'hudson.plugins.git.GitTool'
    git 'https://github.com/kuisathaverat/TestSSLServer.git'
  }
  stage ('Compile sources'){
    //tool name: 'maven3', type: 'hudson.tasks.Maven$MavenInstallation'
    if (isUnix()) {
      sh 'mvn clean compile'
    } else {
      bat 'mvn clean compile'
    }
    
  }
  stage ('Execute Test SSL support features'){
    if (isUnix()){
      sh 'mvn -Djavax.net.debug=ssl:handshake -Dexec.mainClass=org.bolet.TestSSLServer -Dexec.args=${targetHost} exec:java'
    } else {
      bat 'mvn -Djavax.net.debug=ssl:handshake -Dexec.mainClass=org.bolet.TestSSLServer -Dexec.args=%targetHost% exec:java'
    }
    
  }
  stage ('Execute Test SSL handshake'){
    if (isUnix()) {
      sh 'mvn -Djavax.net.debug=ssl:handshake -Dexec.mainClass=org.bolet.TestSSLHandShake -Dexec.args=https://${targetHost} exec:java'
    } else {
      bat 'mvn -Djavax.net.debug=ssl:handshake -Dexec.mainClass=org.bolet.TestSSLHandShake -Dexec.args=https://%targetHost% exec:java'
    }
 }
}