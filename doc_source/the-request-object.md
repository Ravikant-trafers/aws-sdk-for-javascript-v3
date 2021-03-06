--------

This is a preview version of the Developer Guide for the AWS SDK for JavaScript Version 3 \(V3\)\.

A preview version of the AWS SDK for JavaScript V3 is available on [Github](https://github.com/aws/aws-sdk-js-v3)\.

Help us improve the AWS SDK for JavaScript documentation by providing feedback using the **Feedback** link, or create an issue or pull request on [GitHub](https://github.com/awsdocs/aws-sdk-for-javascript-v3)\.

--------

# Creating service client requests<a name="the-request-object"></a>

Making requests to AWS service clients is straightforward\. Version 3 \(V3\) of the SDK for JavaScript enables you to send requests\. 

**Note**  
You can also perform operations using version 2 \(V2\) commands when using the V3 of the SDK for JavaScript\. For more information, see [ Using V2 commands  To use V2 commands in the ^SDK for JavaScript, you import the full AWS Service packages, as demonstrated in the following code\. 

```
const {DynamoDB} = require('@aws-sdk/client-dynamodb');
```  To call V2 commands in the recommended async/await pattern, use the following syntax\.  

```
client.command(parameters)
``` The following example uses the V2 `createBucket` command to create a DynamoDB table using the recommended async/await pattern\. 

```
const {DynamoDB} = require('@aws-sdk/client-dynamodb');
const DymamoDB = new DynamoDB({region: 'us-west-2'});
var tableParams = {
    TableName : TABLE_NAME
};
async function run() => {
      try {
           const data = s3.createTable(tableParams);
           console.log("Success", data);
      } 
      catch (err) {
           console.log("Error", err);
      }
};
run();
``` The following example uses the V2 `createBucket` command to create a DynamoDB table using the recommended async/await pattern\. 

```
const {DynamoDB} = require('@aws-sdk/client-dynamodb');
const DymamoDB = new DynamoDB({region: 'us-west-2'});
var tableParams = {
    TableName : TABLE_NAME
};
async function run() => {
      try {
           const data = s3.createTable(tableParams);
           console.log("Success", data);
      } 
      catch (err) {
           console.log("Error", err);
      }
};
run();
``` The following example uses the V2 `createBucket` command to create a DynamoDB table using the c pattern\. 

```
const {S3} = require('@aws-sdk/client-s3');
const s3 = new S3({region: 'us-west-2'});
var bucketParams = {
    Bucket : BUCKET_NAME
};
function run(){
         s3.createBucket(bucketParams, function(err, data) {
         if (err) {
         console.log("Error", err);
         } else {
         console.log("Success", data.Location);
         }
    })
};
``` ](welcome.md#using_v2_commands)\.

**To send a request:**

1. Initialize a client object with the desired configuration, such as a specific AWS Region\.

1. \(Optional\) Create a request JSON object with the values for the request, such as the name of a specific Amazon S3 bucket\. You can examine the parameters for the request by looking at the API Reference topic for the interface with the name associated with the client method\. For example, if you use the *AbcCommand* client method, the request interface is *AbcInput*\.

1. Initialize a service command, optionally, with the request object as input\.

1. Call `send` on the client with the command object as input\.

For example, to list your Amazon DynamoDB tables in `us-west-2`, you can do it with async/await\.

```
(async function() {
  const { 
    DynamoDBClient, 
    ListTablesCommand 
  } = require('@aws-sdk/client-dynamodb');
  const dbClient = new DynamoDBClient({ region: 'us-west-2' });
  const command = new ListTablesCommand({});

  try {
    const results = await dbClient.send(command);
    console.log(results.TableNames.join('\n'));
  } catch (err) {
    console.error(err);
  }
})();
```