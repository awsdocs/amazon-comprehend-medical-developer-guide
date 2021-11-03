# Step 4: Getting started using the Amazon Comprehend Medical APIs<a name="gettingstarted-api"></a>

The following examples demonstrate how to use Amazon Comprehend Medical operations using the AWS CLI, Java, and Python\. Use them to learn about Amazon Comprehend Medical operations and as building blocks for your own applications\.

To run the AWS CLI and Python examples, install the AWS CLI\. For more information, see [Step 2: Set up the AWS Command Line Interface \(AWS CLI\)](gettingstarted-awscli.md)\.

To run the Java examples, install the AWS SDK for Java\. For instructions for installing the AWS SDK for Java, see [ Set up the AWS SDK for Java](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/setup-install.html)\.

**Topics**
+ [Detecting medical entities using the AWS Command Line Interface](#med-examples-cli)
+ [Detecting medical entities using the AWS SDK for Java](#med-examples-java)
+ [Detecting medical entities using the AWS SDK for Python \(Boto\)](#med-examples-python)

## Detecting medical entities using the AWS Command Line Interface<a name="med-examples-cli"></a>

The following example demonstrates using the `DetectEntitiesV2` operation using the AWS CLI to return the medical entities detected in text\. To run the example, you must install the AWS CLI\. For more information, see [Step 2: Set up the AWS Command Line Interface \(AWS CLI\)](gettingstarted-awscli.md)\.

The example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

```
aws comprehendmedical detect-entities-v2 \
    --endpoint endpoint \
    --region region \
    --text "aspirin is required 20 mg po daily for 2 times as tab"
```

 The response is the following:

```
{
    "Entities": [
        {
            "Category": "MEDICATION", 
            "BeginOffset": 0, 
            "EndOffset": 7, 
            "Text": "aspirin", 
            "Traits": [], 
            "Score": 0.9988090991973877, 
            "Attributes": [
                {
                    "BeginOffset": 20, 
                    "EndOffset": 25, 
                    "Text": "20 mg", 
                    "Traits": [], 
                    "Score": 0.9559056162834167, 
                    "Type": "DOSAGE", 
                    "Id": 1, 
                    "RelationshipScore": 0.9981593489646912
                }, 
                {
                    "BeginOffset": 26, 
                    "EndOffset": 28, 
                    "Text": "po", 
                    "Traits": [], 
                    "Score": 0.9995359182357788, 
                    "Type": "ROUTE_OR_MODE", 
                    "Id": 2, 
                    "RelationshipScore": 0.9969323873519897
                }, 
                {
                    "BeginOffset": 29, 
                    "EndOffset": 34, 
                    "Text": "daily", 
                    "Traits": [], 
                    "Score": 0.9803128838539124, 
                    "Type": "FREQUENCY", 
                    "Id": 3, 
                    "RelationshipScore": 0.9990783929824829
                }, 
                {
                    "BeginOffset": 39, 
                    "EndOffset": 46, 
                    "Text": "2 times", 
                    "Traits": [], 
                    "Score": 0.8623972535133362, 
                    "Type": "DURATION", 
                    "Id": 4, 
                    "RelationshipScore": 0.9996501207351685
                }, 
                {
                    "BeginOffset": 50, 
                    "EndOffset": 53, 
                    "Text": "tab", 
                    "Traits": [], 
                    "Score": 0.784785270690918, 
                    "Type": "FORM", 
                    "Id": 5, 
                    "RelationshipScore": 0.9986748695373535
                }
            ], 
            "Type": "GENERIC_NAME", 
            "Id": 0
        }
    ], 
    "UnmappedAttributes": []
}
```

## Detecting medical entities using the AWS SDK for Java<a name="med-examples-java"></a>

The following example uses the `DetectEntitiesV2` operation with Java\. To run the example, install the AWS SDK for Java\. For instructions on installing the AWS SDK for Java, see [ Set up the AWS SDK for Java](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/setup-install.html)\. 

```
import com.amazonaws.auth.AWSCredentials;
import com.amazonaws.auth.AWSCredentialsProvider;
import com.amazonaws.auth.AWSStaticCredentialsProvider;
import com.amazonaws.auth.BasicAWSCredentials;
import com.amazonaws.client.builder.AwsClientBuilder;
import com.amazonaws.services.comprehendmedical.AWSComprehendMedical;
import com.amazonaws.services.comprehendmedical.AWSComprehendMedicalClient;
import com.amazonaws.services.comprehendmedical.model.DetectEntitiesRequest;
import com.amazonaws.services.comprehendmedical.model.DetectEntitiesResult;
 
public class SampleAPICall {
 
    public static void main() {
 
        AWSCredentialsProvider credentials
                = new AWSStaticCredentialsProvider(new BasicAWSCredentials("YOUR AWS ACCESS KEY", "YOUR AWS SECRET"));
 
        AWSComprehendMedical client = AWSComprehendMedicalClient.builder()
                                                                .withCredentials(credentials)
                                                                .withRegion("YOUR REGION")
                                                                .build();
 
 
        DetectEntitiesV2Request request = new DetectEntitiesV2Request();
        request.setText("cerealx 84 mg daily");
 
        DetectEntitiesV2Result result = client.detectEntitiesV2(request);
        result.getEntities().forEach(System.out::println);
    }
}
```

The output contains the three entities found in the input text, their location in the input text\. A confidence level that the entity was correctly identified is also listed with each entity\. The following output shows the `Generic_Name`, `Dosage`, and `Frequency` entities from the preceding example\.

```
{Id: 0,BeginOffset: 0,EndOffset: 3,Score: 0.9940211,Text: Bob,Category: 
PROTECTED_HEALTH_INFORMATION,Type: NAME,Traits: [],}
{Id: 2,BeginOffset: 23,EndOffset: 30,Score: 0.99914634,Text: aspirin,Category: MEDICATION,Type: GENERIC_NAME,Traits: [],Attributes: 
[{Type: DOSAGE,Score: 0.9630807,RelationshipScore: 0.99969745,Id: 1,BeginOffset: 14,EndOffset: 19,Text: 50 mg,Traits: []}]}
```

## Detecting medical entities using the AWS SDK for Python \(Boto\)<a name="med-examples-python"></a>

The following example uses the `DetectEntitiesV2` operation with Python\. To run the sample, install the AWS CLI\. For more information, see [Step 2: Set up the AWS Command Line Interface \(AWS CLI\)](gettingstarted-awscli.md)\.

```
import boto3
client = boto3.client(service_name='comprehendmedical', region_name='YOUR REGION')
result = client.detect_entities_v2(Text= 'cerealx 84 mg daily')
entities = result['Entities'];
for entity in entities:
    print('Entity:', entity)
```

The output contains the three entities found in the input text, their location in the input text\. A confidence level that the entity was correctly identified is also listed with each entity\. The following output shows the `Generic_Name`, `Dosage`, and `Frequency` entities from the preceding example\.

```
Entity: {
    'Attributes': [
        {
            'BeginOffset': 8,
            'Category': 'MEDICATION',
            'EndOffset': 13,
            'Id': 2,
            'RelationshipScore': 0.9995119571685791,
            'RelationshipType': 'DOSAGE',
            'Score': 0.9337134957313538,
            'Text': '84 mg',
            'Traits': [],
            'Type': 'DOSAGE'
        },
        {
            'BeginOffset': 14,
            'Category': 'MEDICATION',
            'EndOffset': 19,
            'Id': 3,
            'RelationshipScore': 0.998765230178833,
            'RelationshipType': 'FREQUENCY',
            'Score': 0.990627646446228,
            'Text': 'daily',
            'Traits': [],
            'Type': 'FREQUENCY'
        }
    ],
    'BeginOffset': 0,
    'Category': 'MEDICATION',
    'EndOffset': 7,
    'Id': 1,
    'Score': 0.8877692222595215,
    'Text': 'cerealx',
    'Traits': [],
    'Type': 'BRAND_NAME'
}
```
