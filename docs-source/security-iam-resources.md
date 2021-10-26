# Amazon Comprehend Medical API Permissions: actions, resources, and conditions reference<a name="security-iam-resources"></a>

Use the following table as a reference when setting up [Access Control](security-iam.md#access-control-med) and writing a permissions policy that you can attach to an IAM identity \(an identity\-based policy\)\. The list includes each Amazon Comprehend Medical API operation, the corresponding action for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\. 

To express conditions, you can use AWS condition keys in your Amazon Comprehend Medical policies\. For a complete list of keys, see [Available Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
To specify an action, use the `comprehendmedical:` prefix followed by the API operation name, for example, `comprehendmedical:DetectEntities`\.

Use the scroll bars to see the rest of the table\.


**Amazon Comprehend Medical API and Required Permissions for Actions**  

| Amazon Comprehend Medical API Operations | Required Permissions \(API Actions\) | Resources | 
| --- | --- | --- | 
| DescribeEntitiesDetectionV2Job | comprehendmedical:DescribeEntitiesDetectionV2Job | \* | 
| DescribePHIDetectionJob | comprehendmedical:DescribePHIDetectionJob | \* | 
| DetectEntities | comprehendmedical:DetectEntities | \* | 
| DetectEntitiesV2 | comprehendmedical:DetectEntitiesV2 | \* | 
| DetectPHI | comprehendmedical:DetectPHI | \* | 
| ListEntitiesDetectionV2Jobs | comprehendmedical:ListEntitiesDetectionV2Jobs | \* | 
| ListPHIDetectionJobs | comprehendmedical:ListPHIDetectionJobs | \* | 
| StartEntitiesDetectionV2Job | comprehendmedical:StartEntitiesDetectionV2Job | \* | 
| StartPHIDetectionJob | comprehendmedical:StartPHIDetectionJob | \* | 
| StopEntitiesDetectionV2Job | comprehendmedical:StopEntitiesDetectionV2Job | \* | 
| StopPHIDetectionJob | comprehendmedical:StopPHIDetectionJob | \* | 
| InferICD10CM | comprehendmedical:InferICD10CM | \* | 
| InferRxNorm | comprehendmedical:InferRxNorm | \* | 
| StartICD10CMInferenceJob | comprehendmedical:StartICD10CMInferenceJob | \* | 
| StartRxNormInferenceJob | comprehendmedical:StartRxNormInferenceJob | \* | 
| ListICD10CMInferenceJobs | comprehendmedical:ListICD10CMInferenceJobs | \* | 
| ListRxNormInferenceJobs | comprehendmedical:ListRxNormInferenceJobs | \* | 
| StopICD10CMInferenceJob | comprehendmedical:StopICD10CMInferenceJob | \* | 
| StopRxNormInferenceJob | comprehendmedical:StopRxNormInferenceJob | \* | 
| DescribeICD10CMInferenceJob | comprehendmedical:DescribeICD10CMInferenceJob | \* | 
| DescribeRxNormInferenceJob | comprehendmedical:DescribeRxNormInferenceJob | \* | 