# What is Amazon Comprehend Medical?<a name="comprehendmedical-welcome"></a>

Amazon Comprehend Medical detects and returns useful information in unstructured clinical text such as physician's notes, discharge summaries, test results, and case notes\. Amazon Comprehend Medical uses natural language processing \(NLP\) models to detect entities, which are textual references to medical information such as medical conditions, medications, or Protected Health Information\(PHI\)\. For a full list of detected entities, see [Detect entities \(Version 2\)](textanalysis-entitiesv2.md)\. Amazon Comprehend Medical also enables users to link these detected entities to standardized medical knowledge bases such as RxNorm and ICD\-10\-CM through ontology linking operations\. 

 The information in this developer guide is intended for application developers\. This guide includes information about using Amazon Comprehend Medical programmatically through either the AWS CLI or the Amazon Comprehend Medical APIs\. 

Pricing for Amazon Comprehend Medical differs from Amazon Comprehend pricing\. For more information, see [Amazon Comprehend Medical Pricing](https://aws.amazon.com/comprehend/pricing/)\.

**Supported Languages**

 Amazon Comprehend Medical only detects medical entities in English language \(US\-EN\) texts\.

## Important notice<a name="important-notice"></a>

Amazon Comprehend Medical is not a substitute for professional medical advice, diagnosis, or treatment\. Amazon Comprehend Medical provides confidence scores that indicate the level of confidence in the accuracy of the detected entities\. Identify the right confidence threshold for your use case, and use high confidence thresholds in situations that require high accuracy\. In certain use cases, results should be reviewed and verified by appropriately trained human reviewers\. For example, Amazon Comprehend Medical should only be used in patient care scenarios after review for accuracy and sound medical judgment by trained medical professionals\.

## Amazon Comprehend Medical use cases<a name="how-examples-med"></a>

You can use Amazon Comprehend Medical for the following healthcare applications:
+ ** Patient case management and outcome**— Doctors and healthcare providers can manage and easily access medical information that doesn’t fit into traditional forms\. Patients can report their health concerns in a narrative with more information than standard formats\. By analyzing case notes, providers can identify candidates for early screening of medical conditions before the condition becomes more difficult and expensive to treat\. 
+ **Clinical research**—Life sciences and research organizations can optimize the matching process for enrolling patients into clinical trials\. By using Amazon Comprehend Medical to detect pertinent information in clinical text, researchers can improve pharmacovigilance, perform post\-market surveillance to monitor adverse drug events, and assess therapeutic effectiveness by easily detecting vital information in follow\-up notes and other clinical texts\. For instance, it can be easier and more effective to monitor how patients respond to certain therapies by analyzing their narratives\.
+ **Medical billing and healthcare revenue cycle management**—Payors can expand their analytics to include unstructured documents such as clinical notes\. More information about a diagnosis can be analyzed and used to help determine appropriate billing codes from unstructured documents\. Natural language processing \(NLP\) is the most critical component of computer\-assisted coding \(CAC\)\. Amazon Comprehend Medical uses the latest advances in NLP to analyze clinical text, helping to decrease time to revenue and improve reimbursement accuracy\.
+ **Ontology linking **—Use the ontology linking features to detect entities from clinical text and link those entities to standardized concepts in common medical ontologies\. **InferICD10CM** identifies possible medical conditions as entities\. **InferICD10CM** links those entities to unique codes from the 2019 version of [ the International Classification of Diseases, 10th Revision, Clinical Modification \(ICD\-10\-CM\)](https://www.cdc.gov/nchs/icd/icd10cm.htm)\. **InferRxNorm** identifies medications listed in clinical text as entities and links those entities to normalized concept identifiers from [ the RxNorm database from the US National Library of Medicine](https://www.nlm.nih.gov/research/umls/rxnorm/docs/rxnormfiles.html )\. **InferSNOMEDCT** detects medical concepts such as medical conditions and anatomy, medical tests, or treatments and procedures, as entities and links them to codes from the [ Systematized Nomenclature of Medicine, Clinical Terms \(SNOMED CT\)](https://www.snomed.org/snomed-ct/why-snomed-ct) ontology\. 

## Benefits of Amazon Comprehend Medical<a name="how-benefits-med"></a>

Some of the benefits of using Amazon Comprehend Medical include:
+ **Easy, powerful natural language processing integration into your applications**— Use APIs to build text analysis capabilities into your applications for powerful and accurate natural language processing\. 
+ **Accuracy**— Use deep learning technology to accurately analyze text\. Our models are constantly trained with new data across multiple domains to improve accuracy\.
+ **Scalability**— Detect information from multiple documents, making rapid insights into patient health and care possible\.
+ **Integrate with other AWS services**—Amazon Comprehend Medical is designed to work seamlessly with other AWS services like Amazon S3 and AWS Lambda\. Store your documents in Amazon S3, analyze real\-time data with Kinesis Data Firehose, or use Amazon Transcribe to transcribe patient narratives into text that can be analyzed by Amazon Comprehend Medical\. Support for AWS Identity and Access Management \(IAM\) makes it easy to securely control access to Amazon Comprehend Medical operations\. Using IAM, you can create and manage AWS users and groups to grant the appropriate access to your developers and end users\.
+ **Low cost**— Only pay for the documents you analyze\. There are no minimum fees or upfront commitments\. 

## HIPAA compliance<a name="how-medical-hipaa"></a>

This is a HIPAA Eligible Service\. For more information about AWS, U\.S\. Health Insurance Portability and Accountability Act of 1996 \(HIPAA\), and using AWS services to process, store, and transmit protected health information \(PHI\), see [HIPAA Overview](https://aws.amazon.com/compliance/hipaa-compliance/)\.

Connections to Amazon Comprehend Medical containing PHI must be encrypted\. By default, all connections to Amazon Comprehend Medical use HTTPS over TLS\. Amazon Comprehend Medical does not persistently store customer content\. Therefore, you do not need to configure encryption at\-rest within the service\.

## Accessing Amazon Comprehend Medical<a name="accessing-comprehend-medical"></a>

1. AWS Management Console– Provides a web interface that you can use to access Amazon Comprehend Medical\.

1. AWS Command Line Interface \(AWS CLI\) – Provides commands for a broad set of AWS services, including Amazon Comprehend Medical, and is supported on Windows, macOS, and Linux\. For more information about installing the AWS CLI, see AWS Command Line Interface\. 

1. AWS SDKs – AWS provides SDKs \(software development kits\) that consist of libraries and sample code for various programming languages and platforms \(Java, Python, Ruby, \.NET, iOS, Android, etc\.\)\. The SDKs provide a convenient way to create programmatic access to Amazon Comprehend Medical and AWS\. For more information, see AWS SDKs\.

## How to get started with Amazon Comprehend Medical<a name="first-time-user-med"></a>

If you are a first\-time user of Amazon Comprehend Medical, we recommend that you read the following sections in order:

1. [How Amazon Comprehend Medical works](comprehendmedical-howitworks.md) – This section introduces Amazon Comprehend Medical concepts\. 

1. [Getting started with Amazon Comprehend Medical](comprehendmedical-gettingstarted.md) – This section explains how to set up your account and test Amazon Comprehend Medical\. 