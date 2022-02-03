# Text analysis batch APIs<a name="textanalysis-batchapi"></a>

Use Amazon Comprehend Medical to analyze medical text stored in an Amazon S3 bucket\. Analyze up to 10 GB of documents in one batch\. You use the console to create and manage batch analysis jobs, or use batch APIs to detect medical entities, including protected health information \(PHI\)\. The APIs start, stop, list, and describe ongoing batch analysis jobs\.

 Pricing information for batch analysis and other Amazon Comprehend Medical operations can be found [here](https://aws.amazon.com/comprehend/pricing/)\.

## Important notice<a name="important-notice"></a>

The batch analysis operations of Amazon Comprehend Medical are not a substitute for professional medical advice, diagnosis, or treatment\. Identify the right confidence threshold for your use case, and use high confidence thresholds in situations that require high accuracy\. For certain use cases, results should be reviewed and verified by appropriately trained human reviewers\. All operations of Amazon Comprehend Medical should only be used in patient care scenarios after review for accuracy and sound medical judgment by trained medical professionals\.

## Performing batch analysis using the APIs<a name="performing-batch-api"></a>

You can run a batch analysis job using either the Amazon Comprehend Medical console or the Amazon Comprehend Medical Batch APIs\.

**Prerequisites**

 When you are using the Amazon Comprehend Medical API, create an AWS Identity Access and Management \(IAM\) policy and attach it to an IAM role\. To learn more about IAM roles and trust policies, see [IAM Policies and Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)\. 

****

1. Upload your data into an S3 bucket\.

1. To start a new analysis job, use either the StartEntitiesDetectionV2Job operation or the StartPHIDetectionJob operation\. When you start the job, tell Amazon Comprehend Medical the name of the input S3 bucket that contains the input files and designate the output S3 bucket to write the files after batch analysis\.

1. Monitor the progress of the job by using the console or the DescribeEntitiesDetectionV2Job operation or the DescribePHIDetectionJob operation\. Additionally, ListEntitiesDetectionV2Jobs and ListPHIDetectionJobs enable you to see the status of all ontology linking batch analysis jobs\.

1. If you need to stop a job in progress, use StopEntitiesDetectionV2Job or StopPHIDetectionJob to stop analysis\.

1. To view the results of your analysis job, see the output S3 bucket that you configured when you started the job\.

## Performing batch analysis using the console<a name="batch-api-console"></a>

****

1. Upload your data into an S3 bucket\.

1. To start a new analysis job, select the type of analysis you will be performing\. Then provide the name of the S3 bucket that contains the input files and the name of the S3 bucket where you want to send the output files\.

1. Monitor the status of your job while it is ongoing\. From the console, you are can view all batch analysis operations and their status, including when analysis was started and ended\.

1. To see the results of your analysis job, see the output S3 bucket that you configured when you started the job\. 

## IAM Policies for batch operations<a name="batch-iam"></a>

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

## Batch analysis output files<a name="batch-ouput"></a>

Amazon Comprehend Medical creates one output file for each input file in the batch\. The file has the extension `.out`\. Amazon Comprehend Medical first creates a directory in the output S3 bucket using the *AwsAccountId*\-*JobType*\-*JobId* as the name, and then writes all of the output files for the batch to this directory\. Amazon Comprehend Medical creates this new directory so that output from one job does not overwrite the output of another\.

The output from a batch operation produces the same output as a synchronous operation\. For examples of the output generated by Amazon Comprehend Medical, see [Detect entities](textanalysis-entities.md)\.

Each batch operation produces three manifest files that contain information about the job\. 
+ `Manifest` – Summarizes the job\. Provides information about the parameters used for the job, the total size of the job, and the number of files processed\.
+ `success` – Provides information about the files that were successfully processed\. Includes the input and output file name and the size of the input file\.
+ `unprocessed` – Lists files that the batch job did not process\. Typically this is because the file was added to the input directory after the batch job was started\.

Amazon Comprehend Medical writes the files to the output directory that you specified for the batch job\. The following sections show the structure of the manifest files\.

### Batch manifest file<a name="batch-manifest"></a>

The following is the JSON structure of the batch manifest file\.

```
{
  "Summary" : {
    "Status" : "COMPLETED | FAILED | PARTIAL_SUCCESS | STOPPED",
    "JobType" : "DetectEntitiesJob | PHIDetection",
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

### Success manifest file<a name="batch-success"></a>

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

### Unprocessed manifest file<a name="batch-unprocessed"></a>

The following is the JSON structure of the manifest file that contains information about unprocessed files\.

```
{
        "Files": [
               "input path/input file name",
               "input path/input file name"
        ]
}
```