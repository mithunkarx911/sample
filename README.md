# sample
.
U.S. Hospital NPI → EHR Vendor Mapping
Open-source datasets, exact dataset names, fields, joins, 2025–26 coverage, and reproducible linkage workflow
Research reference | Updated August 18, 2026

1. Executive Summary
The objective is to construct a U.S. hospital master table that links a hospital's CMS Certification Number (CCN) and NPI to the certified EHR/health IT product reported by the hospital and then to the EHR developer/vendor. The strongest public-source path is CMS Hospital Promoting Interoperability (PI) → CEHRT ID → ONC CHPL, with CMS Hospital General Information providing the hospital/CCN reference and CMS NPPES providing NPI records.
Important 2025–26 coverage point: the ONC public hospital-to-CHPL linkage dataset currently documented by ONC is the exact dataset named 'Certified Health Information Technology Reported by Hospitals for Promoting Interoperability Performance' and currently has a 2023–2024 date range. CMS has a current 2026 release of the underlying 'Promoting Interoperability - Hospital' dataset. Therefore, a complete 2025–26 hospital → EHR vendor table should not be represented as an already-published ONC 2025–26 linkage. For 2025–26, use the CMS PI Hospital data as the hospital-side source and obtain/resolve the CEHRT IDs against CHPL; if an official ONC 2025 linkage is subsequently released, it should replace the reconstructed linkage.
2. Exact Core Datasets
#
Exact dataset / resource name
Publisher
Purpose
Key information

1
Promoting Interoperability - Hospital
CMS Provider Data Catalog
Hospital-level Medicare PI data; includes CEHRT ID and hospital identifiers.
Facility ID/CCN, CEHRT ID, Facility Name, address, dates

2
Certified Health Information Technology Reported by Hospitals for Promoting Interoperability Performance
ONC Health IT Research & Analysis
Official ONC linkage of hospital PI data to CHPL certified product information; currently 2023–2024.
Facility.ID, CEHRT ID, chpl_id, product_database_id, developer_name, product_name, year

3
Hospital General Information
CMS Provider Data Catalog
Medicare-registered hospital reference table with facility identifiers and hospital characteristics.
facility_id, facility_name, address, citytown, state, zip_code, hospital_type, ownership

4
NPPES Data Dissemination V.2
CMS NPPES
National Provider Identifier reference data. Type 2 organizational NPIs and associated practice locations are especially relevant.
NPI, Legal Business Name, taxonomy, addresses, practice locations, endpoints

5
Certified Health IT Product List (CHPL)
ONC
Authoritative listing of certified health IT products and developers.
CHPL ID/product listing identifiers, developer, product, certification details

3. Dataset 1: Promoting Interoperability - Hospital
Exact dataset name: 'Promoting Interoperability - Hospital'. It is published in the CMS Provider Data Catalog under Hospitals. CMS describes it as hospital-level public reporting for the Medicare Promoting Interoperability Program. The dataset reports the Certified Electronic Health Record Technology (CEHRT) ID and whether the hospital meets the criteria for promoting interoperability.
Exact downloadable CSV filename documented in the CMS Hospital data dictionary:
PROMOTING_INTEROPERABILITY-HOSPITAL.CSV
Important fields
Field
Meaning / role

Facility ID
CMS hospital identifier / CCN used to identify the hospital across CMS hospital datasets.

Facility Name
Hospital name.

Address
Hospital street address.

City/Town
Hospital city.

State
Hospital state/territory.

ZIP Code
Hospital ZIP code.

County/Parish
Hospital county/parish.

Telephone Number
Hospital telephone number.

CEHRT ID
15-character alpha-numeric CMS/ONC Certified EHR Technology identifier reported for the PI performance period.

Meets criteria for promoting interoperability of EHRs
PI program criterion result.

Start Date
Performance/reporting period start date associated with the CEHRT ID.

End Date
Performance/reporting period end date associated with the CEHRT ID.

CMS currently lists the PI Hospital dataset as a hospital dataset and shows a May 13, 2026 release with an April 28, 2026 last-modified date. CMS also states that the PI measure 'Promoting Interoperability CEHRT ID' is updated annually.
4. Dataset 2: Certified Health Information Technology Reported by Hospitals for Promoting Interoperability Performance
Exact ONC dataset name: 'Certified Health Information Technology Reported by Hospitals for Promoting Interoperability Performance'. ONC states that this dataset combines CMS Promoting Interoperability – Hospital data with the ONC Certified Health IT Product List (CHPL). The currently documented date range is 2023–2024, and the page was last updated January 2026.
Exact downloadable file name shown by ONC:
hospital-promoting-interoperability-chpl-linkage [CSV]
Exact linkage fields documented by ONC
Field
What it means
How you use it

Facility.ID
Hospital's CMS Certification Number (CCN), a unique 6-digit identifier for Medicare-participating hospitals.
Primary hospital-side join key to other CMS hospital datasets.

Facility.Name
Hospital name.
Validation / secondary matching.

Address
Hospital street address.
Validation / NPI matching support.

City.Town
Hospital city.
Validation / NPI matching support.

State
Hospital state or territory.
Validation / NPI matching support.

CEHRT ID
15-character identifier generated through the CHPL process and reported by the hospital.
Bridge from hospital PI reporting to CHPL.

chpl_id
Unique CHPL identifier for the certified product listing.
Join to CHPL product information.

product_database_id
Product database identifier used by CHPL public APIs.
API/product-level linkage.

developer_name
Developer associated with the certified product listing.
EHR developer/vendor field.

product_name
Certified product name.
EHR product field.

year
Promoting Interoperability program year.
Time dimension.

Why this dataset is particularly valuable
It does not merely list EHR products. It links the hospital's reported CEHRT information to CHPL product information.
A hospital can have multiple rows because it may report multiple certified products for a performance period.
ONC explicitly identifies Facility.ID/CCN as a common identifier for linking hospitals across health care datasets.
ONC explicitly identifies chpl_id and product_database_id as keys for further CHPL linkage.
ONC notes that a small percentage of CEHRT IDs were invalid and were corrected using fuzzy matching/manual corrections during construction, which makes the official ONC linkage preferable when the relevant year is available.
5. Dataset 3: Hospital General Information
Exact dataset name: 'Hospital General Information'. CMS describes it as a list of all hospitals registered with Medicare, including addresses, phone numbers, hospital type, ownership and other hospital characteristics. The current CMS release has 5,432 rows.
Field
Role in the project

facility_id
CMS hospital facility identifier / CCN; use as the hospital master key.

facility_name
Hospital name.

address
Hospital address.

citytown
City.

state
State.

zip_code
ZIP code.

countyparish
County/parish.

telephone_number
Phone number.

hospital_type
Hospital type.

hospital_ownership
Ownership category.

emergency_services
Emergency services indicator.

6. Dataset 4: NPPES Data Dissemination V.2
Exact CMS resource: 'NPI Files'. The current CMS NPPES download page states that, effective March 3, 2026, NPPES no longer supports Version 1 of the monthly and weekly downloadable files and recommends Version 2 (V.2).
The monthly V.2 dissemination includes three reference files:
Other Name Reference File: additional Other Names associated with Type 2 NPIs.
Practice Location Reference File: all non-primary practice locations associated with Type 1 and Type 2 NPIs.
Endpoint Reference File: all endpoints associated with Type 1 and Type 2 NPIs.
For hospital organization mapping, focus on Type 2 organizational NPIs, then use legal business name, taxonomy, address and practice-location information to associate the NPI with the CMS hospital/CCN. NPPES does not directly contain the hospital's EHR vendor.
7. Dataset 5: Certified Health IT Product List (CHPL)
Exact resource name: 'Certified Health IT Product List (CHPL)'. ONC describes CHPL as the comprehensive and authoritative listing of certified health information technologies successfully tested and certified under the ONC Health IT Certification Program.
CHPL ID identifies a certified product listing.
Developer name identifies the certified health IT developer/vendor associated with the listing.
Product name identifies the certified product.
Product database ID is used by CHPL public APIs to identify unique certified product listings.
CHPL can be searched by developer, product or CHPL ID.
Some withdrawn or terminated certified products can still be relevant to CMS EHR Certification IDs; therefore, certification status may matter when resolving historical CEHRT IDs.
8. The Correct 2025–26 Mapping Architecture
Do not assume there is a single public file containing NPI + hospital + EHR vendor for 2025–26. Build the linkage in stages:
Start with CMS 'Promoting Interoperability - Hospital' for the relevant reporting year and extract Facility ID/CCN and CEHRT ID.
Use CMS 'Hospital General Information' to validate the hospital and retain facility_id, facility_name, address, citytown, state and ZIP.
Resolve each CEHRT ID against ONC CHPL data or the applicable ONC linkage resource.
Retrieve the CHPL ID, product database ID, developer name and product name.
Use CMS NPPES Data Dissemination V.2 to identify the organizational NPI(s) corresponding to the hospital.
Validate NPI-to-hospital matches using legal business name, address, city, state, ZIP, taxonomy and practice-location records.
Create a final hospital master table with one row per hospital-product-year, or a separate hospital-year table with a normalized child table for multiple EHR products.
9. Recommended Final Tables
A normalized design avoids incorrectly forcing hospitals with multiple certified products into one EHR vendor.
Table
Recommended columns

hospital_master
ccn, hospital_name, address, city, state, zip, hospital_type, ownership

hospital_npi
ccn, npi, npi_entity_type, legal_business_name, taxonomy, address, match_method, match_score

hospital_ehr_year
ccn, reporting_year, cehrt_id, start_date, end_date

ehr_product
cehrt_id, chpl_id, product_database_id, developer_name, product_name, certification_status

hospital_ehr_link
ccn, reporting_year, cehrt_id, chpl_id, developer_name, product_name

10. Final Target Output
For downstream analysis, produce a table similar to:
NPI
CCN
Hospital
Year
CEHRT ID
CHPL ID
EHR Product
EHR Vendor
NPI Match

10xxxxxxxxx
123456
Example Hospital
2025
15Exxxxxxxxxxx
xxx
Example EHR Product
Example Developer
Exact/High

10xxxxxxxxx
654321
Example Hospital 2
2025
15Exxxxxxxxxxx
yyy
Example EHR Product 2
Example Developer 2
Exact/High

11. Critical Limitation: NPI Is Not the Hospital-PI Key
The hospital PI/CHPL linkage is based on Facility.ID/CCN and CEHRT ID, not NPI. NPI is supplied separately by NPPES. Therefore, do not join NPI directly to CEHRT ID. First establish a defensible NPI ↔ hospital/CCN relationship, then attach the EHR data.
This matters because a hospital organization can have multiple NPIs, and a health system can contain multiple hospitals. A name-only join can therefore create false vendor assignments.
12. Recommended NPI-to-Hospital Matching Hierarchy
Exact CCN-to-hospital identity from CMS, where a reliable NPI crosswalk is available.
Exact or near-exact legal organization name + full address match.
Organization name + city + state + ZIP match.
Practice-location match for Type 2 NPI.
Taxonomy consistency check.
Phone/address consistency check.
Fuzzy name matching only as a last step, with a recorded match score and manual review for ambiguous cases.
Keep a 'match_method' and 'match_confidence' column. Never silently overwrite ambiguous NPI matches.
13. 2025–26 Coverage Reality
Resource
Current verified coverage/status
Use for 2025–26

ONC Hospital–CHPL linkage
Currently documented as 2023–2024.
Use as the validated model/older linkage; do not label it 2025–26.

CMS Promoting Interoperability - Hospital
Current CMS hospital PI dataset; 2026 release available.
Primary hospital-side source for current/2025-era PI information.

CMS Hospital General Information
Current hospital reference dataset; 2026 release available.
Hospital/CCN reference and validation.

CMS NPPES Data Dissemination V.2
Current monthly/weekly NPI files; V.2 required/recommended from March 2026.
NPI reference.

ONC CHPL
Current authoritative certified-health-IT product list.
Resolve product/developer information from CEHRT/CHPL identifiers.

14. What This Can and Cannot Prove
Question
Can the stack answer it?

Which hospital reported a CEHRT ID?
Yes, from CMS PI Hospital data.

Which certified product corresponds to a CEHRT ID?
Yes, through ONC/CHPL linkage.

Which developer/vendor is associated with the certified product?
Yes, through CHPL developer_name.

Which CCN is the hospital?
Yes, CMS Facility ID/CCN.

What is the hospital's NPI?
Potentially, through NPPES + hospital matching; NPI is not the native PI join key.

Does every hospital have exactly one NPI?
No. Do not assume one-to-one.

Does an EHR vendor prove that a specific CPT/HCPCS code was generated by that vendor?
No. EHR-vendor linkage alone does not establish code-level causation.

Can the stack identify a suspicious CPT/HCPCS coding pattern by vendor?
Potentially, but a claims dataset containing NPI/provider and HCPCS/CPT information is required, plus sufficient observations and appropriate controls.

15. If Your End Goal Is EHR Vendor → CPT/HCPCS Analysis
The hospital-EHR master table should be treated as an attribution layer, not as the coding dataset itself. A defensible downstream pipeline is:
Build hospital CCN ↔ NPI crosswalk.
Build hospital CCN ↔ CEHRT ID ↔ CHPL product ↔ developer/vendor.
Obtain a claims or utilization dataset containing NPI/provider and HCPCS/CPT.
Aggregate codes at the NPI or organization level.
Attach the EHR vendor using the hospital/provider linkage.
Control for specialty, place of service, hospital type, geography, payer and patient/case mix where available.
Only then test whether code distributions differ across EHR vendors.
Important: a statistical association between an EHR vendor and a code does not by itself show that the vendor caused an incorrect CPT/HCPCS code. Vendor attribution is a contextual variable and should be analyzed with appropriate confounder controls.
16. Official Sources and Links
CMS – Promoting Interoperability - Hospital: https://data.cms.gov/provider-data/topics/hospitals/promoting-interoperability
CMS – Hospital General Information: https://data.cms.gov/provider-data/dataset/xubh-q36u
CMS – Hospital data dictionary: https://data.cms.gov/provider-data/sites/default/files/data_dictionaries/hospital/HOSPITAL_Data_Dictionary.pdf
ONC – Hospital CHPL linkage dataset: https://healthit.gov/data/datasets/certified-health-information-technology-reported-by-hospitals-for-promoting-interoperability-performance/
CMS – NPPES NPI Files: https://download.cms.gov/nppes/NPI_Files.html
ONC – Certification of Health IT / CHPL: https://healthit.gov/certification-health-it/
ONC – CHPL Public User Guide: https://healthit.gov/resources/certified-health-it-product-list-chpl-public-user-guide/
ONC – Hospital Certified Health IT Developers Quick Stat: https://healthit.gov/data/quickstats/hospital-health-it-developers/
17. Source Verification Notes
The dataset names and field descriptions in this document were checked against official CMS and ONC pages available as of August 18, 2026. The most important verified facts are: (1) CMS currently publishes 'Promoting Interoperability - Hospital'; (2) the CMS data dictionary documents the file name PROMOTING_INTEROPERABILITY-HOSPITAL.CSV and CEHRT ID; (3) ONC's hospital-to-CHPL linkage is currently documented for 2023–2024; (4) ONC documents Facility.ID as the hospital CCN and chpl_id/product_database_id as CHPL linkage keys; and (5) CMS NPPES currently recommends Version 2 downloadable files.
18. Bottom Line
For a 2025–26 U.S. hospital EHR-vendor master, the core public-source architecture is CMS 'Promoting Interoperability - Hospital' + CMS 'Hospital General Information' + CMS 'NPPES Data Dissemination V.2' + ONC 'Certified Health IT Product List (CHPL)'. The ONC dataset 'Certified Health Information Technology Reported by Hospitals for Promoting Interoperability Performance' is the cleanest official hospital-to-CHPL linkage, but its currently documented coverage is 2023–2024. For 2025–26, reconstruct the linkage from the current CMS PI Hospital CEHRT IDs and CHPL, and clearly label the resulting table as a reconstructed linkage unless/ until ONC publishes the corresponding official year.