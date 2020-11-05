#!groovy
import groovy.json.JsonSlurperClassic
node {

    def BUILD_NUMBER=env.BUILD_NUMBER
    def RUN_ARTIFACT_DIR="tests/${BUILD_NUMBER}"
    def SFDC_USERNAME

    def HUB_ORG=env.HUB_ORG_DH
    def SFDC_HOST = env.SFDC_HOST_DH
    def JWT_KEY_CRED_ID = env.JWT_CRED_ID_DH
    def CONNECTED_APP_CONSUMER_KEY=env.CONNECTED_APP_CONSUMER_KEY_DH
	def FORCE_ORG_URL=env.FORCE_ORG_URL
	
    println 'SECOND' 
    println 'KEY IS' 
    println JWT_KEY_CRED_ID
    println HUB_ORG
    println SFDC_HOST
    println CONNECTED_APP_CONSUMER_KEY
	println FORCE_ORG_URL
    println 'SECOND' 	
    

    withCredentials([file(credentialsId: FORCE_ORG_URL, variable: 'jwt_key_file')]) {
    println jwt_key_file 
        stage('Deploye Code') {
            if (isUnix()) {
		    
                rc = sh returnStatus: true, script: "sfdx force:auth:sfdxurl:store -f ${jwt_key_file}"
            }else{
                 rc = bat returnStatus: true, script: "sfdx force:auth:jwt:grant -auth:jwt:grant --clientid 3MVG9d8..z.hDcPKztkdDe_wTJPooh0gGplHhOJW6AHyKkWpHy3zqhwKrvJR3eJRQjuydD3p14Ktzc1QV3Kwy --jwtkeyfile server.key --username kapiton182@gmail.com --instanceurl https://login.salesforce.com --setdefaultusername"
            }
           
			println rc
			
			if (isUnix()) {
				rmsg = sh returnStdout: true, script: "sfdx force:mdapi:deploy -d /force-app/main/default  -u ${HUB_ORG}"
			}else{
			   rmsg = bat returnStdout: true, script: "sfdx force:mdapi:deploy -d /force-app/main/default/. -u ${HUB_ORG}"
			}
			  
            printf rmsg
            println('Hello from a Job DSL script!')
            println(rmsg)
        }
    }
}