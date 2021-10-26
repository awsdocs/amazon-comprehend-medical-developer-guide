# Text analysis APIs<a name="comprehendmedical-textanalysis"></a>

Amazon Comprehend Medical enables you to examine clinical documents to gain various insights about their content using pre\-trained Natural Language Processing \(NLP\) models\. Analysis can be performed both on single files or as a batch analysis on multiple files stored in an Amazon S3 bucket\.

With Amazon Comprehend Medical, you can perform the following on your documents:
+ [Detect Entities \(Version 2\)](textanalysis-entitiesv2.md) —Examine unstructured clinical text to detect textual references to medical information such as medical condition, treatment, tests and results, and medications\. This version uses a new model and changes the way some entities are returned in the output\. For more information, see \.
+ [Detect PHI ](textanalysis-phi.md)—Examine unstructured clinical text to detect textual references to protected health information \(PHI\) such as names and addresses\.
+ [Detect entities](textanalysis-entities.md)— Examine unstructured clinical text to detect textual references to medical information such as medical condition, treatment, tests and results, and medications\. Use `Detect Entities Version 2 ` for all new applications\.

**Topics**
+ [Detect Entities \(Version 2\)](textanalysis-entitiesv2.md)
+ [Detect entities](textanalysis-entities.md)
+ [Detect PHI](textanalysis-phi.md)
+ [Text analysis batch APIs](textanalysis-batchapi.md)