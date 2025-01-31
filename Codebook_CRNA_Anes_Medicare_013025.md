Codebook for Anesthesia Office Visits for Medicare Pricing
================
Bre Hager Wilhelm

data \<- read.csv(“~/PhD/Data/2024_pdc_s3_ppl_data_anesthesiology.csv”)

## Introduction

This codebook describes the variables used in the analysis of Medicare
pricing data specific to anesthesia providers patient visits –
Anesthesiologists and Certified Registered Nurse Anesthetists. The
dataset contains information on Medicare pricing and copays for new and
established patients, categorized by ZIP code. The variables documented
here include independent, dependent, and control variables relevant to
the study.

## Variables

### Geographic Identifier

- **zip_code**: ZIP code of the location where the Medicare pricing data
  was collected.
  - **Construction**: Five-digit numerical code.
  - **Unit of analysis**: ZIP code level.
  - **Format**: Integer.
  - **Limitations**: ZIP codes may not perfectly align with healthcare
    service areas.
  - **Type**: String (categorical).

### Medicare Pricing for New Patients

- **min_medicare_pricing_for_new_patient**: Minimum Medicare
  reimbursement rate for a new patient visit.
  - **What it measures**: Lowest Medicare reimbursement amount for new
    patients.
  - **Construction**: Derived from Medicare billing data.
  - **Unit of analysis**: Individual ZIP code.
  - **Format**: Float (USD currency).
  - **Limitations**: May not reflect all providers in a region.
  - **Type**: Continuous.
  - **Summary stats**: Mean, median, standard deviation.
- **max_medicare_pricing_for_new_patient**: Maximum Medicare
  reimbursement rate for a new patient visit.
  - **What it measures**: Maximum Medicare reimbursement amount for new
    patients.
  - **Construction**: Derived from Medicare billing data.
  - **Unit of analysis**: Individual ZIP code.
  - **Format**: Float (USD currency).
  - **Limitations**: May not reflect all providers in a region.
  - **Type**: Continuous.
  - **Summary stats**: Mean, median, standard deviation.
- **mode_medicare_pricing_for_new_patient**: Most frequently occurring
  Medicare reimbursement rate for a new patient visit.
  - **Type**: Mode value, categorical representation.

### Copay for New Patients

- **min_copay_for_new_patient**: Minimum out-of-pocket copay required
  for a new patient visit.
- **max_copay_for_new_patient**: Maximum out-of-pocket copay required
  for a new patient visit.
- **mode_copay_for_new_patient**: Most commonly observed copay required
  for a new patient visit.
  - **What they measure**: The minimum, maximum, and most frequent copay
    amounts required for new patient visits.
  - **Unit of analysis**: ZIP code level.
  - **Format**: Float (USD currency).
  - **Limitations**: May not include all insurance providers.
  - **Type**: Continuous.

### Procedure Codes for New Patients

- **most_utilized_procedure_code_for_new_patient**: The most commonly
  billed procedure code for a new patient visit.
  - **What it measures**: The most frequent CPT code used for new
    patient visits.
  - **Format**: String.
  - **Limitations**: May not fully capture variations in procedures
    across providers.
  - **Type**: Categorical.

### Medicare Pricing for Established Patients

- **min_medicare_pricing_for_established_patient**: Minimum Medicare
  reimbursement rate for an established patient visit.
- **max_medicare_pricing_for_established_patient**: Maximum Medicare
  reimbursement rate for an established patient visit.
- **mode_medicare_pricing_for_established_patient**: Most frequently
  occurring Medicare reimbursement rate for an established patient
  visit.
  - **Same description as the new patient version**.

### Copay for Established Patients

- **min_copay_for_established_patient**: Minimum out-of-pocket copay
  required for an established patient visit.
- **max_copay_for_established_patient**: Maximum out-of-pocket copay
  required for an established patient visit.
- **mode_copay_for_established_patient**: Most commonly observed copay
  required for an established patient visit.
  - **Same description as the new patient version**.

### Procedure Codes for Established Patients

- **most_utilized_procedure_code_for_established_patient**: The most
  commonly billed procedure code for an established patient visit.
  - **Same description as the new patient version**.

## Additional Information

- **Dates of observations**: Collected from 2020 - 2024.
- **Data format**: CSV / xlsx
- **Weights**: Not applicable.
- **ID columns**: ZIP code acts as the primary identifier.

## Notes

- This codebook will be updated as needed throughout the semester.
- The dataset is structured at the ZIP code level, with all values
  representing aggregated statistics for that geographic unit.
- The independent variable in this study will be **\[scope of practice
  legislation for nurse anesthetists\]**, and the dependent variable
  will be **\[the cost of anesthesia services\]**.
- This analysis will assess whether expanding the scope of practice for
  nurse anesthetists reduces costs while maintaining or improving access
  to care.
