# Ontology linking batch analysis<a name="ontologies-batchapi"></a>

Use Amazon Comprehend Medical to detect entities in clinical text stored in an Amazon Simple Storage Service \(Amazon S3\) bucket and to link those entities to standardized ontologies\. You can use ontology linking batch analysis to analyze either a collection of documents or a single document with up to 20,000 characters\. By using either the console or the `InferRxNorm` and `InferIC10CM` ontology linking batch APIs, you can perform operations to start, stop, list, and describe ongoing batch analysis jobs\.

 For pricing information for batch analysis and other Amazon Comprehend Medical operations, see [Amazon Comprehend Medical Pricing](https://aws.amazon.com/comprehend/pricing/)\.

## Important notice<a name="important-notice"></a>

Amazon Comprehend Medical ontology linking batch analysis operations are not intended as a substitute for professional medical advice, diagnosis, or treatment\. Identify the right confidence threshold for your use case\. In situations that require great accuracy, use high confidence thresholds\. Use all Amazon Comprehend Medical operations in patient care scenarios only after the results have been reviewed for accuracy and sound medical judgment by trained medical professionals\.

## Performing batch analysis<a name="performing-batch-analysis-ontology-linking"></a>

You can run a batch analysis job using either the Amazon Comprehend Medical console or the Amazon Comprehend Medical Batch APIs\.

### Performing batch analysis using the APIs<a name="batch-api-ontology-linking"></a>

**Prerequisites**

 When you are using the Amazon Comprehend Medical API, create an AWS Identity Access and Management \(IAM\) policy and attach it to an IAM role\. To learn more about IAM roles and trust policies, see [IAM Policies and Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)\. 

****

1. Upload your data into an S3 bucket\.

1. To start a new analysis job, use either the or the operation\. Provide the name of the S3 bucket that contains the input files and the name of the S3 bucket where you want to send the output files\.

1. Monitor the progress of the job by using or operations\. Additionally, and enable you to see the status of all ontology linking batch analysis jobs\.

1. If you need to stop a job in progress, use or to stop analysis\.

1. To view the results of your analysis job, see the output S3 bucket that you configured when you started the job\.

### Performing batch analysis using the console<a name="batch-api-ontology-linking-console"></a>

****

1. Upload your data into an S3 bucket\.

1. To start a new analysis job, select the type of analysis you will be performing\. Then provide the name of the S3 bucket that contains the input files and the name of the S3 bucket where you want to send the output files\.

1. Monitor the status of your job while it is ongoing\. From the console, you are can view all batch analysis operations and their status, including when analysis was started and ended\.

1. To see the results of your analysis job, see the output S3 bucket that you configured when you started the job\. 

## IAM policies for batch operations<a name="batch-iam-ontology-linking"></a>

The IAM role that calls the Amazon Comprehend Medical batch APIs must have a policy that grants access to the S3 buckets that contain the input and output files\. It must also be assigned a trust relationship that enables the Amazon Comprehend Medical service to assume the role\. To learn more about IAM roles and trust policies, see [IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)\.

The role must have the following policy\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::input-bucket/*"
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::input-bucket",
                "arn:aws:s3:::output-bucket",
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "s3:PutObject"
            ],
            "Resource": [
                " arn:aws:s3:::output-bucket/*"
            ],
            "Effect": "Allow"
        }
    ]
}
```

The role must have the following trust relationship\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": [
          "comprehendmedical.amazonaws.com"
        ]
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

## Batch analysis output files<a name="batch-ouput-ontology-linking"></a>

Amazon Comprehend Medical creates one output file for each input file in the batch\. The file has the extension `.out`\. Amazon Comprehend Medical first creates a directory in the output S3 bucket using the *AwsAccountId*\-*JobType*\-*JobId* as the name, and then writes all of the output files for the batch to this directory\. Amazon Comprehend Medical creates this new directory so that output from one job doesn't overwrite the output of another\.

A batch operation produces the same output as a synchronous operation\.

Each batch operation produces three manifest files that contain information about the job:
+ `Manifest` – Summarizes the job\. Provides information about the parameters used for the job, the total size of the job, and the number of files processed\.
+ `Success` – Provides information about the files that were successfully processed\. Includes the input and output file name and the size of the input file\.
+ `Unprocessed` – Lists files that the batch job did not process\. Typically, a file isn't processed because it was added to the input directory after the batch job started\.

Amazon Comprehend Medical writes these files to the output directory that you specified for the batch job\. The following sections show the structure of the manifest files\.

### Batch manifest file<a name="batch-manifest-ontology-linking"></a>

The following is the JSON structure of the batch manifest file\.

```
{
  "Summary" : {
    "Status" : "COMPLETED | FAILED | PARTIAL_SUCCESS | STOPPED",
    "JobType" : "ICD10CMInferenceJob | RxNormInferenceJob",
    "InputDataConfiguration" : {
      "Bucket" : "input bucket",
      "Path" : "path to files/account ID-job type-job ID"
    },
    "OutputDataConfiguration" : {
      "Bucket" : "output bucket",
      "Path" : "path to files"
    },
    "InputFileCount" : number of files in input bucket,
    "TotalMeteredCharacters" : total characters processed from all files,
    "UnprocessedFilesCount" : number of files not processed,
    "SuccessFilesCount" : total number of files processed,
    "TotalDurationSeconds" : time required for processing,
    "SuccessfulFilesListLocation" : "path to file",
    "UnprocessedFilesListLocation" : "path to file"
  }
}
```

### Success manifest file<a name="batch-success-ontology-linking"></a>

The following is the JSON structure of the file that contains information about successfully processed files\.

```
{
        "Files": [{
               "Input": "input path/input file name",
               "Output": "output path/output file name",
               "InputSize": size in bytes of input file
        }, {
               "Input": "input path/input file name",
               "Output": "output path/output file name",
               "InputSize": size in bytes of input file
        }]
}
```

### Unprocessed manifest file<a name="batch-unprocessed-ontology-linking"></a>

The following is the JSON structure of the manifest file that contains information about unprocessed files\.

```
{
        "Files": [
               "input path/input file name",
               "input path/input file name"
        ]
}
```