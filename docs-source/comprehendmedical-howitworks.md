# How Amazon Comprehend Medical works<a name="comprehendmedical-howitworks"></a>

Amazon Comprehend Medical uses a pretrained natural language processing \(NLP\) model to analyze unstructured clinical text through entity detection\. An entity is a textual reference to medical information such as medical conditions, medications, or Protected Health Information \(PHI\)\. Some operations go one step further by detecting entities and then linking those entities to standardized ontologies\. The model is continuously trained on a large body of medical texts, so you don't need to provide training data\. All results include a confidence score, which indicates the confidence that Amazon Comprehend Medical has in the accuracy of the detected entities\. 

Both entity detection and ontology linking can be performed as either synchronous or asynchronous operations:
+ Synchronous operations— Enables analysis on single documents which return the results of the analysis directly to your applications\. Use the single\-document operations when you are creating an interactive application that works on one document at a time\. 
+ Asynchronous operations — Enables analysis on a collection or batch of documents stored in an Amazon S3 bucket\. The results of the analysis are returned in an S3 bucket\.

**Note**  
Amazon Comprehend Medical can analyze only text in English \(US\-EN\)\.

## Synchronous entity detection<a name="detect-individual"></a>

The and operations detect entities in unstructured clinical text from individual documents\. You send a document to the Amazon Comprehend Medical service and receive the results of the analysis in the response\. 

## Asynchronous batch analysis<a name="detect-multiple"></a>

The and operations start asynchronous jobs to detect references to medical information such as medical condition, treatment, tests and results or protected health information that is stored in an Amazon S3 bucket\. The output of the detection job is written to a separate Amazon S3 bucket from which it can be used for further processing or downstream analysis\. 

The , and operations start ontology linking batch operations which detect entities and link those entities to standardized codes in the RxNorm and ICD\-10\-CM knowledge bases\. 

## Ontology linking<a name="link-standard"></a>

 The and operations detect potential medical conditions and medications and link them to codes in the ICD\-10\-CM and RxNorm knowledge bases, respectively\. You can use ontology linking batch analysis to analyze either a collection of documents or a single large document with up to 20,000 characters\. By using either the console or the InferRxNorm and InferIC10CM ontology linking batch APIs, you can perform operations to start, stop, list, and describe ongoing batch analysis jobs\. 

### Linking to concepts in the ICD\-10\-CM knowledge base of medical conditions<a name="link-ICD10CM"></a>

The `InferICD10CM` operation detects potential medical conditions and links them to codes from the 2019 version of the International Classification of Diseases, 10th Revision, Clinical Modification \(ICD\-10\-CM\)\. For each potential medical condition detected, Amazon Comprehend Medical lists the matching ICD\-10\-CM codes and descriptions\. Listed medical conditions in the results include a confidence score, which indicates the confidence that Amazon Comprehend Medical has in the accuracy of the entities to the matched concepts in the results\.  

### Linking to concepts in the RxNorm knowledge base of medications<a name="link-rxnorm"></a>

The `InferRxNorm` operation identifies medications that are listed in a patient record as entities\. It links entities to concept identifiers \(RxCUI\) from the RxNorm database from the National Library of Medicine\. Each RxCUI is unique for different strengths and dose forms\. Listed medications in the results include a confidence score, which indicates the confidence that Amazon Comprehend Medical has in the accuracy of the entities matched to the concepts from the RxNorm knowledge base\. Amazon Comprehend Medical lists the top RxCUIs that potentially match for each medication that it detects in descending order based on confidence score\.

