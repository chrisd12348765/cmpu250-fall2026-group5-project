# Codebook

## Original HMDA variables

| Variable | Type | Description | Values / units |
|---|---|---|---|
| `activity_year` | Integer | Year the application was acted on | 2025 for every row |
| `state_code` | String | Two-letter state abbreviation | `NY` for every row |
| `lei` | String | Legal Entity Identifier, a unique ID for the lender | 3 distinct lenders |
| `action_taken` | Integer | Lender's final decision on the application | 1 = Loan originated; 2 = Approved but not accepted by the applicant; 3 = Application denied |
| `derived_race` | String | Applicant race, as derived by the CFPB from the applicant and any co-applicant | White; Asian; Black or African American; American Indian or Alaska Native; Native Hawaiian or Other Pacific Islander; 2 or more minority races; Joint (applicant and co-applicant of different races, one of them White); Free Form Text Only; Race Not Available |
| `derived_ethnicity` | String | Applicant ethnicity, as derived by the CFPB from the applicant and any co-applicant | Hispanic or Latino; Not Hispanic or Latino; Joint (one Hispanic or Latino applicant and one not); Free Form Text Only; Ethnicity Not Available |
| `applicant_age` | String | Age range of the main applicant | <25, 25-34, 35-44, 45-54, 55-64, 65-74, >74; 8888 = not applicable |
| `loan_type` | Integer | Type of loan | 1 = Conventional (not government-insured); 2 = FHA-insured; 3 = VA-guaranteed |
| `debt_to_income_ratio` | String | Applicant's monthly debt payments divided by monthly income | Ranges (<20%, 20%-<30%, 30%-<36%, 50%-60%, >60%), plus single whole-number values from 36 to 49. 23 missing. |
| `derived_msa-md` | Integer | Metropolitan Statistical Area / Metropolitan Division code of the property | 5-digit code; 99999 = not in a metro area |
| `county_code` | Integer | 5-digit FIPS code for the property's county | State code (36) + county code |
| `census_tract` | Integer | 11-digit FIPS code for the property's census tract | State + county + tract |
| `income` | Float | Gross annual income relied on by the lender | Thousands of dollars (e.g., 173 = $173,000). 395 missing. 10 rows are negative, which HMDA allows. |
| `loan_amount` | Integer | Amount of the loan applied for | Dollars, rounded by HMDA to the midpoint of the nearest $10,000 range |
| `tract_minority_population_percent` | Float | Percent of the census tract's population that is a racial or ethnic minority | 0–100 |
| `tract_to_msa_income_percentage` | Integer | Tract median family income as a percent of the metro area's median family income | Percent (100 = same as the metro median). 62 rows are 0, likely meaning not available. |
| `tract_population` | Integer | Total population of the census tract | Persons |

## Variables created for this project

| Variable | Type | How it was created | Values |
|---|---|---|---|
| `denied` | Integer (0/1) | Outcome variable. 1 if `action_taken` = 3 (denied); 0 if `action_taken` = 1 or 2 (approved). | 0 = Approved; 1 = Denied |
| `age_band` | String | Copy of `applicant_age`, with the code 8888 relabeled as `Missing` | <25, 25-34, 35-44, 45-54, 55-64, 65-74, >74, Missing |
| `dti_band` | String | `debt_to_income_ratio` grouped into consistent ranges. The single values 36–49 are combined into 36%-49%. Missing values are labeled `Missing`. | <20%, 20%-<30%, 30%-<36%, 36%-49%, 50%-60%, >60%, Missing |
| `tract_minority_band` | String | `tract_minority_population_percent` grouped into 20-point ranges | 0–<20%, 20–<40%, 40–<60%, 60–<80%, 80–100% |
