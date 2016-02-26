/**
  Workfow to download and execute a SSL Test connexion
  @author kuisatahverat
 **/
 env.targetHost = targetHost
 stage 'Env'
 node {
    sh 'export'
 }

 stage 'Download sources'
 node {
    tool name: 'Default', type: 'hudson.plugins.git.GitTool'
    git 'https://github.com/kuisathaverat/TestSSLServer.git'
 }
 stage 'Compile sources'
 node {
    //tool name: 'maven3', type: 'hudson.tasks.Maven$MavenInstallation'
    sh 'mvn clean compile'
 }
 stage 'Execute Test SSL support features'
 node {
    sh 'mvn -Djavax.net.debug=ssl:handshake -Dexec.mainClass=org.bolet.TestSSLServer -Dexec.args=${targetHost} exec:java'
 }
 stage 'Execute Test SSL handshake'
 node {
    sh 'mvn -Djavax.net.debug=ssl:handshake -Dexec.mainClass=org.bolet.TestSSLHandShake -Dexec.args=https://${targetHost} exec:java'
 }
