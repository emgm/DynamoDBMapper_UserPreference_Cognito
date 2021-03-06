Running the UserPreference OM Sample
============================================
This sample demonstrates how Android can interact with Amazon DynamoDB to store user preferences. For a detailed description of the code, open and read the UserPreference.html file.

1. Import the DynamoDBMapper_UserPreference_Cognito project into Android Studio.
   - From the Welcome screen, click on "Import project".
   - Browse to the DynamoDBMapper_UserPreference_Cognito directory and press OK.
   - Accept the messages about adding Gradle to the project.
   - If the SDK reports some missing Android SDK packages (like Build Tools or the Android API package), follow the instructions to install them.

1. This sample requires Cognito to authorize to Amazon DynamoDB to post content.  Use Amazon Cognito to create a new identity pool:
	1. In the [Amazon Cognito Console](https://console.aws.amazon.com/cognito/), press the `Manage Federated Identities` button and on the resulting page press the `Create new identity pool` button.
	
	1. Give your identity pool a name and ensure that `Enable access to unauthenticated identities` under the `Unauthenticated identities` section is checked.  This allows the sample application to assume the unauthenticated role associated with this identity pool.  Press the `Create Pool` button to create your identity pool.

		**Important**: see note below on unauthenticated user access.

	1. As part of creating the identity pool, Cognito will setup two roles in [Identity and Access Management (IAM)](https://console.aws.amazon.com/iam/home#roles).  These will be named something similar to: `Cognito_PoolNameAuth_Role` and `Cognito_PoolNameUnauth_Role`.  You can view them by pressing the `View Details` button.  Now press the `Allow` button to create the roles.
	1. Save the `Identity pool ID` value that shows up in red in the "Getting started with Amazon Cognito" page, it should look similar to: `us-east-1:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" and note the region that is being used.  These will be used in the application code later.
	1. Now we will attach a policy to the unauthenticated role which has permissions to access the required Amazon DynamoDB API.  This is done by attaching an IAM Policy to the unauthenticated role in the [IAM Console](https://console.aws.amazon.com/iam/home#roles).  First, search for the unauth role that you created in step 3 above (named something similar to `Cognito_PoolNameUnauth_Role`) and select its hyperlink.  In the resulting "Summary" page press the `Attach Policy` button in the "Permissions" tab.
	1. Search for "dynamo" and check the box next to the policy named `AmazonDynamoDBFullAccess` and then press the `Attach Policy` button.  This policy allows the application to perform all operations on the Amazon DynamoDB service.

		More information on AWS IAM roles and policies can be found [here](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage.html).  More information on Amazon DynamoDB policies can be found [here](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/authentication-and-access-control.html).

		**Note**: to keep this example simple it makes use of unauthenticated users in the identity pool.  This can be used for getting started and prototypes but unauthenticated users should typically only be given read-only permissions in production applications.  More information on Cognito identity pools including the Cognito developer guide can be found [here](http://aws.amazon.com/cognito/).


2. Update your App configuration:
   * Update the **IDENTITY_POOL_ID**, **COGNITO_REGION**, **DYNAMODB_REGION** and **TEST_TABLE_NAME** fields in
Constants.java.  For **IDENTITY_POOL_ID** use the value you saved in the step above.  Change **COGNITO_REGION** to the your Cognito region.  For **TEST_TABLE_NAME** just pick any name you want for your database table, the app will create it and set **DYNAMODB_REGION** to the region that your Dynamo DB table is in.

3. Run the project.
