Product: WSO2 ESB Connector for SugarCRM + Integration Tests

Pre-requisites:

	- Maven 3.x
	- Java 1.6 or above

Tested Platform: 

	- Microsoft WINDOWS V-7
	- Ubuntu 13.04
	- WSO2 ESB 4.8.1
		  
STEPS:

	1. To build the connector without running tests from any location, run maven build with the -Dmaven.test.skip=true switch.

	2. Before attempting to run integration tests, uncomment the following in pom.xml (Integration_Test/products/esb/4.8.1/modules/integration/connectors):

		<parent>
        	<groupId>org.wso2.esb</groupId>
        	<artifactId>esb-integration-tests</artifactId>
        	<version>4.8.1</version>
        	<relativePath>../pom.xml</relativePath>
    	</parent>


	3. Make sure the ESB 4.9.0-ALPHA zip available at "{<ESB_CONNECTORS_HOME>/repository/"}

	4. Copy SugarCRM connector zip file (sugarcrm.zip) to the location "Integration_Test/products/esb/4.8.1/modules/integration/connectors/repository/"

	5. Copy the test packages 'sugarcrm-connector-test/src/test/java/org/wso2/carbon/connector/integration/test/common' and 'sugarcrm-connector-test/src/test/java/org/wso2/carbon/connector/integration/test/sugarcrm' to "Integration_Test/products/esb/4.8.1/modules/integration/connectors/src/test/java/org/wso2/carbon/connector/integration/test/"

	6. Make sure the SugarCRM test suite is enabled (as given below) and all other test suites are commented in the following file - "Integration_Test/products/esb/4.8.1/modules/integration/connectors/src/test/resources/testng.xml"  
		<test name="SugarCRM-Connector-Test" preserve-order="true" verbose="2">
			<packages>
				<package name="org.wso2.carbon.connector.integration.test.sugarcrm"/>
			</packages>
		</test>

	7. Obtain a trial sugarCRM account if the given trial account is expired, by using the following steps.
			
		i) Login to https://www.sugarcrm.com.

			When creating a trial login, select the deployment region as 'North America' as the integration test results are compared against the pre-defined dataset of that region.
			In case if you need to support for 'Europe' deployment region, you need to modify the request parameters as per the pre-defined dataset of that region. (e.g. Module Ids)
			
			Note: This account is subjected to expire within 7 days. At the event of expiration the user needs to re-register for another trial account.

		ii) In order to change the default password of the admin, follow the steps below:
			a) Select admin profile (e.g. The admin controls all aspects of Sugar) from the dashboard of the trial account
			b) Select profile option from the top right corner of the screen
			c) Click on 'Edit' and  then select 'Password' tab 
			d) Set Current password, New password and Confirm Password
			e) Click on Save
			
		iii) Convert your password (which was set in above step) to MD5 hash code and change appUri, userName and password (MD5 hash code) appropriately on file at 
			 "sugarcrm-connector-test/src/test/resources/artifacts/ESB/connector/config/sugarcrm.properties" and copy the file to location "Integration_Test/products/esb/4.8.1/modules/integration/connectors/src/test/resources/artifacts/ESB/connector/config/".
       
   	8. Make sure that the yelp connector is set as a module in esb-connectors parent pom.
               <module>sugarcrm/sugarcrm-connector/sugarcrm-connector-1.0.0</module>

    9. Navigate to "<ESB_Connector_Home>" and run the following command.
                $ mvn clean install
