# SNOMED CT linking<a name="ontology-linking-snomed"></a>

 Use **InferSNOMEDCT** to detect medical entities and link them to concepts from the 2021\-03 version of the Systematized Nomenclature of Medicine, Clinical Terms \(SNOMED CT\)\. SNOMED CT provides a comprehensive vocabulary of medical concepts, including medical conditions and anatomy, as well as medical tests, treatments, and procedures\. To learn more about SNOMED CT, visit [ SNOMED CT](https://www.snomed.org/snomed-ct/why-snomed-ct)\. 

For each detected medical entity, Amazon Comprehend Medical lists the top five SNOMED CT concept IDs and descriptions associated with the medical concept, along with a confidence score to indicate the confidence of the model in its prediction\. They are listed in descending order of confidence along with the confidence scores\. The SNOMED CT concept IDs can then be used to structure patient clinical data for medical coding, reporting, or clinical analytics when used with the SNOMED CT polyhierarchy\.

**InferSNOMEDCT** is available for customers in the United States\. For information on SNOMED CT in other countries, and information on SNOMED CT licensing, see [ SNOMED CT](https://www.snomed.org/snomed-ct/why-snomed-ct)\.

**InferSNOMEDCT** is well suited for the following scenarios:
+  Assistance for professional medical coding in patient records 
+  Clinical studies and trials 
+  Population health management

**InferSNOMEDCT** detects entities in the following categories\. Additional contextual information is also detected and linked as attributes or traits\.
+ `MEDICAL_CONDITION` The signs, symptoms, and diagnosis of medical conditions\. 
+ `ANATOMY` The parts of the body or body systems and the locations of those parts or systems\.
+ `TEST_TREATMENT_PROCEDURE` The procedures that are used to determine a medical condition\.

**Important**  
The **InferSNOMEDCT** operation of Amazon Comprehend Medical is not a substitute for professional medical advice, diagnosis, or treatment\. All operations of Amazon Comprehend Medical should only be used in patient care scenarios after review for accuracy and sound medical judgment by trained medical professionals\. 

## Medical condition category<a name="snomed-med-cond"></a>

The `Medical_Condition` category detects the signs, symptoms, and diagnosis of medical conditions\.

### Type<a name="med-cond-type-snomed"></a>

For the **MEDICAL\_CONDITION** category, the following type is detected:
+ `DX_NAME:` An identification of a medical condition that is determined by evaluation of the symptoms\. 

### Attributes<a name="med-cond-attributes-snomed"></a>

The following attributes are detected for the `MEDICAL_CONDITION` category:
+ `ACUITY:` Determination of disease instance, such as chronic, acute, sudden, persistent, or gradual\.
+ `QUALITY:` Any descriptive term of the medical condition, such as stage or grade\. 
+ `DIRECTION`: Directional terms\. For example, left, right medial, lateral, upper, lower, posterior, anterior, distal, proximal, contralateral, bilateral, ipsilateral, dorsal, or ventral\.
+ `SYSTEM_ORGAN_SITE`: Body systems, anatomic locations or regions, and body sites\.

### Traits<a name="med-cond-traits"></a>

The following traits are detected for the `MEDICAL_CONDITION` category:
+ `Diagnosis:` A medical condition that is determined as the cause or result of the symptoms\. Symptoms can be found through physical findings, laboratory or radiological reports, or any other means\. 
+ `Negation:` An indication that a medical condition is not present\.
+ `Sign:` A medical condition that is reported by the physician\.
+ `Symptom:` A medical condition reported by the patient\.

## Anatomy category<a name="anatomy-snomed"></a>

The `ANATOMY` category detects references to the parts of the body or body systems and the locations of those parts or systems\. 

### Attributes<a name="anatomy-attributes-snomed"></a>

The following attributes are detected for the `ANATOMY` category:
+ `DIRECTION`: Directional terms\. For example, left, right medial, lateral, upper, lower, posterior, anterior, distal, proximal, contralateral, bilateral, ipsilateral, dorsal, or ventral\.
+ `SYSTEM_ORGAN_SITE`: Body systems, anatomic locations or regions, and body sites\.

## Test, treatment, procedure category<a name="ttt-snomed"></a>

The `TEST_TREATMENT_PROCEDURE` category detects the procedures that are used to determine a medical condition\. 

### Type<a name="ttt-type-snomed"></a>

For the **TEST\_TREATMENT\_PROCEDURE** category, the following types are detected:
+ `PROCEDURE_NAME:` Interventions performed on the patient to treat a medical condition or to provide patient care\.
+ `TEST_NAME:` Procedures performed on a patient for diagnosis, measurement, screening, or a rating that might have a resulting value\. This includes any procedure, process, evaluation, or rating to determine a diagnosis, to rule out or find a condition, or to scale or score a patient\. 
+ `TREATMENT_NAME:` Interventions performed to combat a disease or disorder\. This includes medications, such as antivirals and vaccinations\.

### Attributes<a name="ttt-attributes-snomed"></a>

For the **TEST\_TREATMENT\_PROCEDURE** category, the following attributes are detected:
+ `TEST_NAME:` The diagnostic test performed\.
+ `TEST_VALUE:` The numeric results from a diagnostic test\. 
+ `TEST_UNIT:` The units associated with a `TEST_VALUE:` result\.
+ `PROCEDURE_NAME:` The name of a surgery or medical procedure performed\. 
+ `TREATMENT_NAME:` The name of a treatment administered to a patient\.

## SNOMED CT details<a name="snomed-details"></a>

Included in the JSON response are the SNOMED CT details, which includes the following information\.
+ `EDITION:` Only the US edition is supported\.
+ `VERSIONDATE: ` The datestamp of the SNOMED CT version used\. 
+ `LANGUAGE:` Analysis on English \(US\-EN\) is supported\.

## Input and response examples<a name="snomed-example"></a>

The following example shows how the `InferSNOMEDCT` operation works\. The following is an example input text\.

 "BHEENT : Boggy inferior turbinates, No oropharyngeal lesion" 

For this example input text, the `InferSNOMEDCT` operation returns the following output\. 

```
{
    "Entities": [
        {
            "Category": "ANATOMY",
            "BeginOffset": 0,
            "EndOffset": 5,
            "Text": "HEENT",
            "Traits": [],
            "SNOMEDCTConcepts": [
                {
                    "Code": "69536005",
                    "Score": 0.8183674812316895,
                    "Description": "Head structure (body structure)"
                },
                {
                    "Code": "429031000124106",
                    "Score": 0.8062137961387634,
                    "Description": "Review of systems, head, ear, eyes, nose and throat (procedure)"
                },
                {
                    "Code": "385383008",
                    "Score": 0.7023276090621948,
                    "Description": "Ear, nose and throat structure (body structure)"
                },
                {
                    "Code": "64237003",
                    "Score": 0.6886451840400696,
                    "Description": "Structure of left half of head (body structure)"
                },
                {
                    "Code": "113028003",
                    "Score": 0.6595167517662048,
                    "Description": "Ear, nose and throat examination (procedure)"
                }
            ],
            "Score": 0.9941003918647766,
            "Attributes": [],
            "Type": "SYSTEM_ORGAN_SITE",
            "Id": 0
        },
        {
            "Category": "MEDICAL_CONDITION",
            "BeginOffset": 8,
            "EndOffset": 33,
            "Text": "Boggy inferior turbinates",
            "Traits": [
                {
                    "Score": 0.916421115398407,
                    "Name": "SIGN"
                }
            ],
            "SNOMEDCTConcepts": [
                {
                    "Code": "254477009",
                    "Score": 0.3194539248943329,
                    "Description": "Tumor of inferior turbinate (disorder)"
                },
                {
                    "Code": "260762006",
                    "Score": 0.2589553892612457,
                    "Description": "Choroidal invasion status (attribute)"
                },
                {
                    "Code": "2455009",
                    "Score": 0.2561122477054596,
                    "Description": "Revision of lumbosubarachnoid shunt (procedure)"
                },
                {
                    "Code": "19883003",
                    "Score": 0.25573015213012695,
                    "Description": "Atrophy of nasal turbinates (disorder)"
                },
                {
                    "Code": "256723009",
                    "Score": 0.2551479935646057,
                    "Description": "Inferior turbinate flap (substance)"
                }
            ],
            "Score": 0.8120518326759338,
            "Attributes": [
                {
                    "Category": "ANATOMY",
                    "RelationshipScore": 0.9952282905578613,
                    "EndOffset": 5,
                    "Text": "HEENT",
                    "Traits": [],
                    "SNOMEDCTConcepts": [
                        {
                            "Code": "69536005",
                            "Score": 0.8183674812316895,
                            "Description": "Head structure (body structure)"
                        },
                        {
                            "Code": "429031000124106",
                            "Score": 0.8062137961387634,
                            "Description": "Review of systems, head, ear, eyes, nose and throat (procedure)"
                        },
                        {
                            "Code": "385383008",
                            "Score": 0.7023276090621948,
                            "Description": "Ear, nose and throat structure (body structure)"
                        },
                        {
                            "Code": "64237003",
                            "Score": 0.6886451840400696,
                            "Description": "Structure of left half of head (body structure)"
                        },
                        {
                            "Code": "113028003",
                            "Score": 0.6595167517662048,
                            "Description": "Ear, nose and throat examination (procedure)"
                        }
                    ],
                    "Score": 0.9941003918647766,
                    "RelationshipType": "SYSTEM_ORGAN_SITE",
                    "Type": "SYSTEM_ORGAN_SITE",
                    "Id": 0,
                    "BeginOffset": 0
                }
            ],
            "Type": "DX_NAME",
            "Id": 1
        },
        {
            "Category": "ANATOMY",
            "BeginOffset": 23,
            "EndOffset": 33,
            "Text": "turbinates",
            "Traits": [],
            "SNOMEDCTConcepts": [
                {
                    "Code": "310607007",
                    "Score": 0.38427865505218506,
                    "Description": "Sarcoidosis of inferior turbinates (disorder)"
                },
                {
                    "Code": "80153006",
                    "Score": 0.35948991775512695,
                    "Description": "Segmented neutrophil (cell)"
                },
                {
                    "Code": "46607005",
                    "Score": 0.34975120425224304,
                    "Description": "Nasal turbinate structure (body structure)"
                },
                {
                    "Code": "6553002",
                    "Score": 0.3453119397163391,
                    "Description": "Inferior nasal turbinate structure (body structure)"
                },
                {
                    "Code": "254477009",
                    "Score": 0.34111809730529785,
                    "Description": "Tumor of inferior turbinate (disorder)"
                }
            ],
            "Score": 0.6760638356208801,
            "Attributes": [],
            "Type": "SYSTEM_ORGAN_SITE",
            "Id": 3
        },
        {
            "Category": "ANATOMY",
            "BeginOffset": 39,
            "EndOffset": 52,
            "Text": "oropharyngeal",
            "Traits": [],
            "SNOMEDCTConcepts": [
                {
                    "Code": "31389004",
                    "Score": 0.8781343102455139,
                    "Description": "Oropharyngeal structure (body structure)"
                },
                {
                    "Code": "33431000119109",
                    "Score": 0.865419328212738,
                    "Description": "Lesion of oropharynx (disorder)"
                },
                {
                    "Code": "263376008",
                    "Score": 0.7922793626785278,
                    "Description": "Entire oropharynx (body structure)"
                },
                {
                    "Code": "716151000",
                    "Score": 0.7752759456634521,
                    "Description": "Structure of oropharynx and/or hypopharynx and/or larynx (body structure)"
                },
                {
                    "Code": "764786007",
                    "Score": 0.7574880719184875,
                    "Description": "Oropharyngeal (intended site)"
                }
            ],
            "Score": 0.33921703696250916,
            "Attributes": [],
            "Type": "SYSTEM_ORGAN_SITE",
            "Id": 5
        },
        {
            "Category": "MEDICAL_CONDITION",
            "BeginOffset": 39,
            "EndOffset": 59,
            "Text": "oropharyngeal lesion",
            "Traits": [
                {
                    "Score": 0.925685465335846,
                    "Name": "SIGN"
                }
            ],
            "SNOMEDCTConcepts": [
                {
                    "Code": "31389004",
                    "Score": 0.8340228199958801,
                    "Description": "Oropharyngeal structure (body structure)"
                },
                {
                    "Code": "33431000119109",
                    "Score": 0.830550491809845,
                    "Description": "Lesion of oropharynx (disorder)"
                },
                {
                    "Code": "764786007",
                    "Score": 0.7099332213401794,
                    "Description": "Oropharyngeal (intended site)"
                },
                {
                    "Code": "418664002",
                    "Score": 0.6987537741661072,
                    "Description": "Oropharyngeal route (qualifier value)"
                },
                {
                    "Code": "110162001",
                    "Score": 0.6958084106445312,
                    "Description": "Abrasion of oropharynx (disorder)"
                }
            ],
            "Score": 0.8390859961509705,
            "Attributes": [
                {
                    "Category": "ANATOMY",
                    "RelationshipScore": 0.9978047013282776,
                    "EndOffset": 5,
                    "Text": "HEENT",
                    "Traits": [],
                    "SNOMEDCTConcepts": [
                        {
                            "Code": "69536005",
                            "Score": 0.8183674812316895,
                            "Description": "Head structure (body structure)"
                        },
                        {
                            "Code": "429031000124106",
                            "Score": 0.8062137961387634,
                            "Description": "Review of systems, head, ear, eyes, nose and throat (procedure)"
                        },
                        {
                            "Code": "385383008",
                            "Score": 0.7023276090621948,
                            "Description": "Ear, nose and throat structure (body structure)"
                        },
                        {
                            "Code": "64237003",
                            "Score": 0.6886451840400696,
                            "Description": "Structure of left half of head (body structure)"
                        },
                        {
                            "Code": "113028003",
                            "Score": 0.6595167517662048,
                            "Description": "Ear, nose and throat examination (procedure)"
                        }
                    ],
                    "Score": 0.9941003918647766,
                    "RelationshipType": "SYSTEM_ORGAN_SITE",
                    "Type": "SYSTEM_ORGAN_SITE",
                    "Id": 0,
                    "BeginOffset": 0
                }
            ],
            "Type": "DX_NAME",
            "Id": 4
        }
    ],
    "SNOMEDCTDetails": {
        "Edition": "US",
        "VersionDate": "20200901",
        "Language": "en"
    },
    "Characters": {
        "OriginalTextCharacters": 59
    },
    "ModelVersion": "0.0.1"
}
```