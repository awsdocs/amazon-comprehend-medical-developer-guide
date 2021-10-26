# Guidelines and quotas<a name="comprehendmedical-quotas"></a>

Keep in mind the following information when using Amazon Comprehend Medical\.

## Important notice<a name="important-notice-x1"></a>

Amazon Comprehend Medical is not a substitute for professional medical advice, diagnosis, or treatment\. Amazon Comprehend Medical provides confidence scores that indicate the level of confidence in the accuracy of the detected entities\. Identify the right confidence threshold for your use case, and use high confidence thresholds in situations that require high accuracy\. For certain use cases, results should be reviewed and verified by appropriately trained human reviewers\. Use Amazon Comprehend Medical in patient care scenarios only after trained medical professionals have reviewed results for accuracy and sound medical judgment\.

## Supported regions<a name="limits-regions-med"></a>

For a list of AWS Regions where Amazon Comprehend Medical is available, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#comprehend-med_region) in the *Amazon Web Services General Reference*\.

## Throttling<a name="limits-throttling-med"></a>

For information about throttling and quotas for Amazon Comprehend Medical, and to request a quota increase, see [AWS Service Quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html )\. 

## Overall quotas<a name="limits-all-med"></a>

Character encoding for Amazon Comprehend Medical is in UTF\-8\. Amazon Comprehend Medical operations have the following quotas for transactions per second\(TPS\) or characters per second \(CPS\):


| Resource | Default | 
| --- | --- | 
| Transactions per second \(TPS\) for the DetectEntities\-v2, DetectEntities, DetectPHI, InferRxNorm, and InferICD10CM operations  | 100 | 
| Characters per second \(CPS\) for the DetectEntities\-v2, DetectEntities, DetectPHI, InferRxNorm, and InferICD10CM operations  | 40,000 | 
| Transactions per second \(TPS\) for the StartEntitiesDetectionV2Job, StartPHIDetectionJob, StopEntitiesDetectionV2Job, StopPHIDetectionJob, StartICD10CMInferenceJob, StartRxNormInferenceJob, StopICD10CMInferenceJob, and StopRxNormInferenceJob operations  | 5 | 
| Transactions per second \(TPS\) for the ListEntitiesDetectionV2Jobs, ListPHIDetectionJobs, DescribeEntitiesDetectionV2Job, DescribePHIDetectionJob, ListICD10CMInferenceJobs, ListRxNormInferenceJobs, DescribeICD10CMInferenceJob, and DescribeRxNormInferenceJob operations  | 10 | 

The size quotas for files as is shown in the table below:


| Description | Quota | 
| --- | --- | 
| Maximum document size \(UTF\-8 characters\) for DetectEntities, DetectEntities\-v2 and DetectPHI operations\. | 20,000 bytes | 
| Maximum document size \(UTF\-8 characters\) for InferICD10\-CM and InferRxNorm operation | 10,000 bytes | 
| Maximum size of text analysis batch jobs \(all files\) | 10 Gb | 
| Maximum size of ontology linking batch analysis jobs \(all files\) | 5 Gb | 
| Minimum size of batch jobs \(all files\) | 1 byte | 
| Maximum individual file size for batch jobs | 40 Kb | 
| Maximum number of files for batch jobs | 5 million | 

 If your text is larger than the character quotas, use [segment\.py](samples/segment.py.zip) to create smaller segments that can be analyzed\.

Only documents in English \(EN\) are supported\.