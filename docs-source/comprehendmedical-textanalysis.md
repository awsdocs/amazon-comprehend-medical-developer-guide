# Text analysis APIs<a name="comprehendmedical-textanalysis"></a>

Amazon Comprehend Medical enables you to examine clinical documents to gain various insights about their content using pre\-trained Natural Language Processing \(NLP\) models\. Analysis can be performed both on single files or as a batch analysis on multiple files stored in an Amazon S3 bucket\.

With Amazon Comprehend Medical, you can perform the following on your documents:
+ [Detect entities \(Version 2\)](textanalysis-entitiesv2.md) —Examine unstructured clinical text to detect textual references to medical information such as medical condition, treatment, tests and results, and medications\. This version uses a different model than the original Detect entities API, and there are a few changes in the output\.
+ [Detect PHI ](textanalysis-phi.md)—Examine unstructured clinical text to detect textual references to protected health information \(PHI\) such as names and addresses\.
+ [Detect entities](textanalysis-entities.md)— Examine unstructured clinical text to detect textual references to medical information such as medical condition, treatment, tests and results, and medications\. Use `Detect entities Version 2 ` for all new applications\.

**Topics**
+ [Detect entities \(Version 2\)](textanalysis-entitiesv2.md)
+ [Detect entities](textanalysis-entities.md)
+ [Detect PHI](textanalysis-phi.md)
+ [Text analysis batch APIs](textanalysis-batchapi.md)