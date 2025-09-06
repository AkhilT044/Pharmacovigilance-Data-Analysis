# [cite_start]"README.DOC" FILE FOR THE QUARTERLY DATA EXTRACT (QDE) FROM THE FDA ADVERSE EVENT REPORTING SYSTEM (FAERS) [cite: 2]

[cite_start]**IMPORTANT:** [cite: 1]

### [cite_start]U.S. FOOD AND DRUG ADMINISTRATION (FDA) [cite: 3]
### [cite_start]CENTER FOR DRUG EVALUATION AND RESEARCH (CDER) [cite: 3]
### [cite_start]OFFICE OF SURVEILLANCE AND EPIDEMOLOGY (OSE) [cite: 3]

[cite_start]**LAST REVISED: February 2022** [cite: 4]

[cite_start]This document describes significant changes resulting from FDA's transition from Legacy AERS (LAERS) to the new FDA AERS (FAERS) database and the modernization of FAERS at FDA. [cite: 5] [cite_start]We have added data to the FAERS database structure and have made minor changes to existing field contents. [cite: 6] [cite_start]Users of the Quarterly Data Extract (QDE) should review all of the changes to the new extract before loading the files into their systems. [cite: 7]

## [cite_start]TABLE OF CONTENTS [cite: 8]
[cite_start]A. INTRODUCTION [cite: 9, 10]
[cite_start]B. CLINICAL CAVEATS [cite: 11]
[cite_start]C. CAVEATS for Users who are Converting from LAERS to FAERS [cite: 12]
[cite_start]D. HOW THE FILES ARE ORGANIZED [cite: 13]
[cite_start]E. FILE NAME NOMENCLATURE [cite: 14]
[cite_start]F. ASCII FILES [cite: 15, 16]
[cite_start]G. XML FILES [cite: 17]
[cite_start]H. QUESTIONS, COMMENTS [cite: 18]
[cite_start]I. REVISION HISTORY [cite: 18]

---

## [cite_start]A. INTRODUCTION [cite: 19, 20]

[cite_start]You are reading the README.DOC file that accompanies the Quarterly Data Extract from the FDA Adverse Event Reporting System (FAERS). [cite: 21] [cite_start]FAERS is a computerized database for the spontaneous reporting of adverse events and medication errors involving human drugs and therapeutic biological products. [cite: 22] [cite_start]FAERS began on September 10, 2012, and replaced the Adverse Event Reporting System (also known as Legacy AERS), which was decommissioned on August 27, 2012. [cite: 23] (For more information on FAERS, please see: [http://www.fda.gov/Drugs/GuidanceComplianceRegulatory Information/Surveillance/Adverse DrugEffects/default.htm](http://www.fda.gov/Drugs/GuidanceComplianceRegulatory%20Information/Surveillance/Adverse%20DrugEffects/default.htm)[cite_start]) [cite: 23, 24]

[cite_start]Each extract covers reports received by FAERS during one quarter of the Year. [cite: 25] [cite_start]An exception is the first FAERS extract which was a non-standard quarter from August 28, 2012 to December 31, 2012, the time period from the decommissioning of LAERS until the end of the fourth quarter of 2012. [cite: 26] [cite_start]The first extract also included Periodic (Non-Expedited) reports from the July/August 2012 time period. [cite: 27] [cite_start]In November 2021 FAERS was modernized and this document reflects the changes. [cite: 28] [cite_start]The forth quarter of 2021 is the first extract to be published under the modernized FAERS system. [cite: 29]

[cite_start]The data are provided in two distinct formats in the extract: [cite: 30]

1. [cite_start]ASCII files, in which data elements are separated from each other by a `$` sign ("$ delimited"). [cite: 32] [cite_start]Please refer to the `ASC NTS.DOC` file for additional information on this format. [cite: 33]
2. [cite_start]XML files conforming to the guidelines of the International Conference on Harmonisation (ICH) concerning transmission of Individual Case Safety Reports (ICSR). [cite: 34, 35] [cite_start]Please refer to the `XML_NTS.DOC` file for additional information on this format. [cite: 35, 36]

[cite_start]Although an effort has been made to make the ASCII consistent with the XML output file, some of the data elements represented in XML are not represented in ASCII, and a few of the data elements represented in ASCII are not represented in XML. [cite: 37] [cite_start]This is due to the very different natures of the two formats and to the fact that ICH E2b/M2 specifically defines the allowable data elements for XML. [cite: 38] [cite_start]Furthermore, neither the ASCII nor the XML is intended to include all possible data fields. [cite: 39]

[cite_start]If you wish to obtain individual case reports through the Freedom of Information Act (FOIA), please refer to these reports by the case report number only. [cite: 40] [cite_start]The request must identify each case report you are interested in receiving. [cite: 41] [cite_start]The case report number is included in the field/data element labeled: (1) `"CASE"` in the AERS ASCII format, (2) `"CASEID"` in the FAERS ASCII format (data files starting the 4th quarter 2012), or (3) `"safetyreportid"` in the SGML/XML format of the quarterly data files. [cite: 42]

---

## [cite_start]B. CLINICAL CAVEATS [cite: 43]

[cite_start]**Disclaimer:** Submission of a safety report does not constitute an admission that medical personnel, user facility, importer, distributor, manufacturer or product caused or contributed to the event. [cite: 44] [cite_start]The information in these reports has not been scientifically or otherwise verified as to a cause and effect relationship and cannot be used to estimate the incidence of these events. [cite: 45]

[cite_start]There are some important things to keep in mind when reviewing or analyzing FAERS data: [cite: 46]

* [cite_start]For any given report, there is no certainty that a suspected drug caused the reaction. [cite: 47] [cite_start]This is because physicians are encouraged to report suspected reactions; however, the event may have been related to the underlying disease being treated, or caused by some other drug being taken concurrently, or simply occurred by chance at that time. [cite: 48, 49]
* [cite_start]Accumulated reports cannot be used to calculate incidence (occurrence rates) or to estimate drug risk. [cite: 50]
* [cite_start]Comparisons between drugs cannot be made from these data. [cite: 51]

[cite_start]The Event code provided in the Reaction file `DRUG REC ACT` Column in the ASCII extract is provided to indicate that the specific Event reoccurred when one of the Suspect Drugs was reintroduced. [cite: 52] [cite_start]The listing of this Event can therefore be associated with any of the listed Suspect drugs in the case. [cite: 53]

[cite_start]**NOTE:** Cases submitted in Paper format (e.g., MedWatch 3500A) will not display an Event code for this `DRUG REC ACT` ASCII data element; instead QDE users should use the Rechallenge value "Y" in the DRUG file as an indicator that the reactions listed in the case reoccurred when one of the Suspect drugs was reintroduced. [cite: 55, 56, 58] [cite_start]Cases submitted in E2B format will provide specific Events that reoccurred (Positive Rechallenge) when one of the Suspect drugs was reintroduced. [cite: 59]

---

## [cite_start]C. CAVEATS for Users who are Converting from LAERS to FAERS [cite: 63]

[cite_start]The following notes are intended to assist users in transitioning their IT systems from LAERS to FAERS. [cite: 64] [cite_start]Users should take into account the following IT and data changes while importing the new FAERS QDE files: [cite: 65]

[cite_start]While the previous LAERS database was Individual Safety Report (ISR) based, the new FAERS database is Case/Version based. [cite: 67] [cite_start]In LAERS, a Case consisted of one or more ISRS (that is, Initial and Follow-up reports), and each ISR number represented a separate version of a case. [cite: 66, 68] [cite_start]So a case could contain multiple ISRS within it, and the latest ISR represented the most current information about a particular case. [cite: 68] [cite_start]However in FAERS, the ISR concept is no longer being employed, and instead, each unique submission of a case received is given a version number (for example, Case# 1234567, Version 1). [cite: 68] [cite_start]The first Version received (formerly called Initial) will be version 1; the second Version received (formerly called Follow-up 1) will be version 2, and so on. [cite: 69] [cite_start]The latest version of a case represents the most current information about a particular Case. [cite: 69] [cite_start]As a result, the FAERS QDE output files will always provide the latest, most current, Version of a Case available at the time the QDE is run. [cite: 69]

... (Additional detailed caveats from the document) ...

[cite_start]In the ASCII `AGE` field, users may occasionally encounter large numeric age values because some manufacturers submit the patient age in DAYS, even for adult patients. [cite: 98] [cite_start]For example, a 30-year (YR) old will be displayed as a 10,950-day (DY) old. [cite: 99] [cite_start]Therefore, users should note the `AGE UNIT` accompanying the large `AGE` value and account for ages not listed with the year (YR) age unit. [cite: 100]

[cite_start]In the XML and ASCII extracts, the new XML tag `<occurcountry>` and the new ASCII field `OCCR_COUNTRY`, respectively, capture the country where the reaction/event occurred. [cite: 106] [cite_start]The new tag and field will allow you to distinguish between domestic and foreign cases. [cite: 108, 109]

---

## [cite_start]D. HOW THE FILES ARE ORGANIZED [cite: 114]

[cite_start]The Quarterly Data Extract contains the following: [cite: 115]

1. [cite_start]`ASCII`, which contains the ASCII data and informational files. [cite: 116]
2. [cite_start]`XML`, which contains the XML data and informational files. [cite: 117]
3. [cite_start]`README.DOC`, the informational file you are now reading. [cite: 118]
4. [cite_start]`FAQS` Frequently Asked Questions. [cite: 119, 120]

---

## [cite_start]E. FILE NAME NOMENCLATURE [cite: 121]

[cite_start]In the ASCII format, file names have the format `<file-descriptor>yyQq`, where `<file-descriptor>` is a 4-letter abbreviation for the data source, 'yy' is a 2-digit identifier for the year, 'Q' is the letter Q, and 'q' is a 1-digit identifier for the quarter. [cite: 122, 123] [cite_start]As an example, the ASCII demographic file for the 4th quarter of 2012 is represented as `DEMO1204`. [cite: 124]

---

## [cite_start]F. ASCII FILES [cite: 128]

[cite_start]The ASCII data files are `$` delimited; that is, a `$` is used to separate the data fields. [cite: 130]

1. [cite_start]`DEMOyyQq.TXT` contains patient demographic and administrative information, a single record for each event report. [cite: 133]
2. [cite_start]`DRUGyyQq.TXT` contains drug/biologic information for as many medications as were reported for the event (1 or more per event). [cite: 134]
3. [cite_start]`REACyyQq.TXT` contains all "Medical Dictionary for Regulatory Activities" (MedDRA) terms coded for the event (1 or more). [cite: 136]
4. [cite_start]`OUTCyyQq.TXT` contains patient outcomes for the event (0 or more). [cite: 139]
5. [cite_start]`RPSRyyQq.TXT` contains report sources for event (0 or more). [cite: 140]
6. [cite_start]`THERyyQq.TXT` contains drug therapy start dates and end dates for the reported drugs (0 or more per drug per event). [cite: 141]
7. [cite_start]`INDIyyQq.TXT` contains all "Medical Dictionary for Regulatory Activities" (MedDRA) terms coded for the indications for use (diagnoses) for the reported drugs (0 or more per drug per event). [cite: 142, 143]

---

## [cite_start]G. XML FILES [cite: 150]
... (Content about XML files) ...

---

## [cite_start]H. QUESTIONS, COMMENTS [cite: 157]
[cite_start]Questions or comments may be directed to the Food and Drug Administration, Center for Drug Evaluation and Research, Office of Surveillance and Epidemiology (301-796-2360 or cderosetracking@fda.hhs.gov). [cite: 158]

---

## [cite_start]I. REVISION HISTORY [cite: 160]
... (Content about revision history) ...

[cite_start]Added new field for Age Group (AGE GRP) field in ASCII Demographic file and new tag (`<patientagegroup>`) added to XML extract populated with Age Group code, when available, as follows: [cite: 171]

| [cite_start]CODE [cite: 172] | [cite_start]MEANING TEXT [cite: 172] |
| :--- | :--- |
| [cite_start]"N" [cite: 172] | [cite_start]"Neonate" [cite: 172] |
| [cite_start]"I" [cite: 172] | [cite_start]"Infant" [cite: 172] |
| [cite_start]"C" [cite: 172] | [cite_start]"Child" [cite: 172] |
[cite_start]| [cite: 172] | [cite_start]"Adolescent" [cite: 172] |
| [cite_start]"A" [cite: 172] | [cite_start]"Adult" [cite: 172] |
| [cite_start]"E" [cite: 172] | [cite_start]"Elderly" [cite: 172] |

[cite_start]Modified field header from `GNDR COD` to `SEX` in ASCII Demographic file. [cite: 178]

[cite_start]In Q4 2021, the FAERS system was modernized, and the data was migrated to a new database. [cite: 184]
