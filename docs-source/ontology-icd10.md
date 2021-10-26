# ICD\-10\-CM linking<a name="ontology-icd10"></a>

 Use **InferICD10CM** to detect possible medical conditions as entities and link them to codes from the 2021 version of [ the International Classification of Diseases, 10th Revision, Clinical Modification \(ICD\-10\-CM\)](https://www.cdc.gov/nchs/icd/icd10cm.htm)\. The ICD\-10\-CM is provided by the US Centers for Disease Control and Prevention \(CDC\)\.

For each detected potential medical condition, Amazon Comprehend Medical lists the matching ICD\-10\-CM codes and descriptions\. They are listed in descending order of confidence along with the confidence scores\. The scores indicate the confidence in the accuracy of the entities matched to the concepts\. Use the ICD\-10\-CM codes for downstream analysis\. Related information such as signs, symptoms, and negation are recognized as traits\. Additional information such as anatomical designations and acuity are listed as attributes\.

**InferICD10CM** is well suited for the following scenarios:
+  Assistance for professional medical coding for patient records 
+  Clinical studies and trials 
+  Integration with a medical software system 
+  Early detection and diagnosis 
+  Population health management 

## Important notice<a name="important-notice"></a>

The **InferICD10CM** operation of Amazon Comprehend Medical is not a substitute for professional medical advice, diagnosis, or treatment\. Identify the right confidence threshold for your use case, and use high confidence thresholds in situations that require high accuracy\. All operations of Amazon Comprehend Medical should only be used in patient care scenarios after review for accuracy and sound medical judgment by trained medical professionals\.

## ICD\-10\-CM category<a name="icd10-cm-category"></a>

**InferICD10CM** detects entities in the `MEDICAL_CONDITION` category\. Additional related information is also detected and linked as attributes or traits\.

## ICD\-10\-CM type<a name="icd10-cm-type"></a>

 **InferICD10CM** detects entities of the types `DX_NAME` and `TIME_EXPRESSION`\.

## ICD\-10\-CM traits<a name="icd10-cm-traits"></a>

**InferICD10CM** detects the following contextual information as traits: 
+ `Diagnosis:` An identification of a medical condition that is determined by evaluation of the symptoms\.
+ `Negation:` An indication that a medical condition is not present\.
+ `Sign:` A medical condition that is reported by the physician\.
+ `Symptom:` A medical condition reported by the patient\.

## ICD\-10\-CM attributes<a name="icd10-cm-attributes"></a>

**InferICD10CM** detects the following contextual information as attributes: 
+ `DIRECTION:` Directional terms\. For example, left, right medial, lateral, upper, lower, posterior, anterior, distal, proximal, contralateral, bilateral, ipsilateral, dorsal, or ventral\.
+ `SYSTEM, ORGAN or SITE:` Anatomical location\.
+ `ACUITY:` Determination of disease instance, such as chronic, acute, sudden, persistent, or gradual\. This only applies to the MEDICAL\_CONDITION type\. 

## Time expression category<a name="time-expression-icd10-cm"></a>

The `TIME_EXPRESSION` category detects entities related to time\. This includes entities such as dates and time expressions such as "three days ago," "today," "currently," "day of admission," "last month," or "16 days\." Results in this category are only returned if they are associated with an entity\. For example, "Yesterday, the patient was diagnosed with influenza " would return Yesterday as a `TIME_EXPRESSION` entity that overlaps with `DX_NAME` entity "influenza\." However, "yesterday" would not be recognized as an entity in "yesterday, the patient walked their dog\." 

## Types<a name="time-expression-icd10cm-categories"></a>

The recognized type of `TIME_EXPRESSION` is `TIME_TO_DX_NAME`: The date a medical condition occurred\. The attribute for this type is `DX_NAME`\.

## Relationship type<a name="time-expression-icd10cm-relationship-type"></a>

The `RELATIONSHIP_TYPE` refers to the relationship between an entity and an attribute\. The recognized `RELATIONSHIP_TYPE` is: `OVERLAP` – The `TIME_EXPRESSION` concurs with the entity detected\.

## Input and response examples<a name="icd10cminput-med"></a>

The following example shows how the `InferICD10CM` operation works\. The following is an example input text\.

 "The patient is a 71\-year\-old female patient of Dr\. X\. The patient presented to the emergency room last evening with approximately 7\- to 8\-day history of abdominal pain which has been persistent\. She has had no nausea and vomiting, but has had persistent associated anorexia\. She is passing flatus, but had some obstipation symptoms with the last bowel movement two days ago\. She denies any bright red blood per rectum and no history of recent melena\. Her last colonoscopy was approximately 5 years ago with Dr\. Y\. She has had no definite fevers or chills and no history of jaundice\. The patient denies any significant recent weight loss\." 

For the input text, the `InferICD10CM` operation returns the following output \(abbreviated for brevity\)\. 

```
{
    "Entities": [
        {
            "Id": 1,
            "Text": "abdominal pain",
            "Category": "MEDICAL_CONDITION",
            "Type": "DX_NAME",
            "Score": 0.9606665968894958,
            "BeginOffset": 153,
            "EndOffset": 167,
            "Attributes": [
                {
                    "Type": "ACUITY",
                    "Score": 0.764342725276947,
                    "RelationshipScore": 0.9999940395355225,
                    "Id": 2,
                    "BeginOffset": 183,
                    "EndOffset": 193,
                    "Text": "persistent",
                    "Traits": []
                }
            ],
            "Traits": [
                {
                    "Name": "SYMPTOM",
                    "Score": 0.7559975981712341
                }
            ],
            "ICD10CMConcepts": [
                {
                    "Description": "Unspecified abdominal pain",
                    "Code": "R10.9",
                    "Score": 0.7775180339813232
                },
                {
                    "Description": "Epigastric pain",
                    "Code": "R10.13",
                    "Score": 0.6876822710037231
                },
                {
                    "Description": "Lower abdominal pain, unspecified",
                    "Code": "R10.30",
                    "Score": 0.6758853197097778
                },
                {
                    "Description": "Generalized abdominal pain",
                    "Code": "R10.84",
                    "Score": 0.6746202707290649
                },
                {
                    "Description": "Upper abdominal pain, unspecified",
                    "Code": "R10.10",
                    "Score": 0.6702126860618591
                }
            ]
        }
...
    "ModelVersion": "0.1.0"
}
```

I`nferICD10CM` also recognizes when an entity is negated in text\. For instance, if a patient is not experiencing a symptom, both the symptom and negation are identified as traits and listed with a confidence score\. Based on the input for the previous example, the symptom `Nausea` would be listed under `NEGATION` because the patient isn't experiencing nausea\. 

```
    {
            "Id": 3,
            "Text": "nausea",
            "Category": "MEDICAL_CONDITION",
            "Type": "DX_NAME",
            "Score": 0.9962648749351501,
            "BeginOffset": 210,
            "EndOffset": 216,
            "Attributes": [],
            "Traits": [
                {
                    "Name": "SYMPTOM",
                    "Score": 0.9296342730522156
                },
                {
                    "Name": "NEGATION",
                    "Score": 0.9620923399925232
                }
            ],
            "ICD10CMConcepts": [
                {
                    "Description": "Nausea with vomiting, unspecified",
                    "Code": "R11.2",
                    "Score": 0.8000147938728333
                },
                {
                    "Description": "Nausea",
                    "Code": "R11.0",
                    "Score": 0.7653312683105469
      }
```