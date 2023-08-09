[![N|Solid](https://brand.autodesk.com/app/uploads/2021/04/alternate-logo-1.svg)](https://www.google.com/url?sa=i&url=https%3A%2F%2Fbrand.autodesk.com%2Fbrand-system%2Flogo%2F&psig=AOvVaw3uZeNJq7-r_3BVMP4cCkjz&ust=1690731812300000&source=images&cd=vfe&opi=89978449&ved=0CBEQjRxqFwoTCNCEsvqgtIADFQAAAAAdAAAAABAE)
# KPI NPS Report
## _July 2023_
#### [Version 3.0](https://github.com/Roco0816/MKDOCS_AD)

## 1. Key Insights
- ![Total_Qualtrics_ID vs Fiscal_Year](https://res.cloudinary.com/dffvrw1wk/image/upload/v1690742152/002_fgcmpv.jpg)
- ![Total_Qualtrics_ID vs Fiscal_Year](https://res.cloudinary.com/dffvrw1wk/image/upload/v1690742564/003_gnaube.jpg)
- ![Total_Qualtrics_ID vs Fiscal_Year](https://res.cloudinary.com/dffvrw1wk/image/upload/v1690743312/004_zq4bg9.jpg)
 - Achievements:
    - The total number of **survey responses** have **increased** year on year since 2020 from **35 to over 100** in 2023. This is a **positive** result and an **investigation** as to what is working successfully can drive **further results**.
    -  The **overall EBA NPS** of **60** indicates a **highly positive sentiment** among **employees** who have access to our products or services. 
    - Leveraging this positive sentiment can contribute to a **positive work environment** and potentially boost employee **engagement and productivity**.
    - Engagement in survey reponses is **highest in the architecture industry**.
    - **Geo_1** has **the highest NPS**, indicating a higher level of **customer loyalty and satisfaction** compared to the other locations.
- Improvements:
    - The majority of respondents are **unique customers** with an **unknown industry**. Investigate to identify these industries. 
    - Improve survey participation and engagement, especially in **construction and product design industries**.
    - **Geo_3** has **the lowest NPS**, suggesting there is room for improvement in **customer sentiment** in this area.
    -  An **overall NPS of 35 out of 100** shows signs of improvement to be made in the **product/process/company**.
    - We can **leverage NPS tables** to facilitate in-depth **analysis** by exploring **NPS scores** alongside specific customer attributes, gaining insights into **customer feedback** and **loyalty** based on different dimensions.

    # 1.1 KPI Business Use Cases
- Tracking NPS allows us to see how much our customers would recommend our product/service/the company to someone else
- We can track this KPI over periods of time and determine whether customer satisfaction with the product/service is improving or declining
- We can leverage this information to enhance our service and identify strengths for further improvement

# 1.2. Document Goals
   - Summarize NPS significance for leadership
   - Document usage and calculation for analysts
   - Describe SQL-based Net Promoter Score (NPS) calculation

# 2. Definition of the KPI

## 2.1 Metric Details

| Item | Details |
| ------ | ------ |
| Metric Title | Net Promoter Score (NPS) |
| Metric Short Description | NPS |
| Metric Long Description | Net Promoter Score |
| Metric SME | Jasson Ji |
| Product Owner | Uddipan |
| Documentation Status | IN PROGESS |

## 2.2 NPS Definition 
NPS stands for Net Promoter Score, a metric used in customer experience programmes. NPS measures the loyalty of customers to a company. NPS scores are measured with a single question survey and reported with a number from -100 to +100. A higher score is desirable. 

![Total_Qualtrics_ID vs Fiscal_Year](https://res.cloudinary.com/dffvrw1wk/image/upload/v1690790058/nps_rrarle.jpg)


# 3. Required KPI Data Sources


Metric Granularity:

- Qualtrics_ID

## 3.1 Segments (Dimensions /Filters / Slicers)
1. Country
2. Customer Size
3. Customer Tenure
4. Geo
5. Industry Group
6. License Compliance ( WIP)
7. Named account
8. Named Account Group
9. Customer Tenure
10. Premium ( WIP)

## 3.2 Caveats & Clarifications


1. **Not all Qualtrics_id have an account_csn, hence not all qualtrics_id will have an account_name**

    **Explanation:**
    
    - Some survey responses in Qualtrics lack linked customer accounts, possibly due to anonymous or non-customer respondents.

    **Impact:**
    
    - Because of this, when analyzing the survey data, there may be cases where the "account_name" field is empty or NULL for certain survey responses, while others will have valid account names associated with them.
    
    **Action:**
        
     -  Filter out non-account holder responses and handle them separately in survey results.
    
2. **Autodesk (ADSK_BUSINESS_SCORE) has its own unique NPS thresholds:**

   - "PROMOTER" are anyone who scores between 6-10 
   - "DETRACTOR" are anyone who scores between 0-3 
   - "OTHERS" are anyone who scores between 4-5
![Total_Qualtrics_ID vs Fiscal_Year](https://res.cloudinary.com/dffvrw1wk/image/upload/v1690790156/nps_002_e04bip.jpg)


3. **Some columns exclusively belong to EBA or NON-EBA, hence field EBA_FLAG is crucial for data navigation**

    **Explanation:**

   - Certain columns in the data are specific to either EBA (Employee-Based Access) or NON-EBA. The "EBA_FLAG" column is used to differenciate between these two data types.

4. **As of 31/07/2023, about 1850 qualtrics_id have multiple ACCOUNT_CSN mapped to them**

   - Some of these CSN's have multiple ACCOUNT_NAME, INDUSTRY & GEO, or multiple values in one of these filters. To ensure consistency, any qualtrics_id with multiple ACCOUNT_CSN will have ACCOUNT_NAME, INDUSTRY, and GEO set to 'UNKNOWN'.

   - This approach helps maintain data clarity and reliability, standardizing the data to 'UNKNOWN' for ambiguous survey responses with multiple possible mappings to different customer accounts or information. It ensures consistent handling during analysis and reporting.

## 3.4 Known Issues
The metric knowledge is being consolidated, gathering inputs from various experts to ensure a comprehensive understanding and informed decision-making based on combined expertise of the SMEs.

## 4. Data Processing Details

**How to Find the Table(s):**
1. Go to the Data Warehouse.
2. Search for the "ENGAGEMENT_SHARED" schema or database.
3. Look for the tables named:
   - "X_PUBLISH"
   - "X_ADSK__MEMBERS"
   - "NPS_X_ADSK_TEAM_MEMBERS"
   - "NPS_NON_X_KEY_DRIVER_PRODUCTS"
   - "NPS_PRODUCTS_ENGMNT"
   
   **Note:** 
    - Some of these tables have different access roles (X_RO_GROUP), indicating permissions or restrictions on who can access them.
   - Each dataset will be updated daily at 07:30 UTC.
   - Some roles require admin rights to access certain tables

| Data Warehouse | Schema/Database | View/Table | Roles with Access | Time Partitions |
| ------ | ------ | ------ | ------ | ------ |
| X_PUBLISH | ENGAGEMENT_SHARED | X_ADSK__MEMBERS | X _RO_GROUP | Not Applicable |
| X_PUBLISH | ENGAGEMENT_SHARED | NPS_X _ADSK_TEAM_MEMBERS | X _RO_GROUP | Not Applicable |
| X_PUBLISH | ENGAGEMENT_SHARED | NPS_NON_X_KEY_DRIVER_PRODUCTS | X _RO_GROUP | Not Applicable |
| X_PUBLISH | ENGAGEMENT_SHARED | NPS_PRODUCTS_ENGMNT | X _RO_GROUP | Not Applicable |

# 5. Sample SQL Queries
## 5.1 Use Case 1
### *_To fetch non-EBA Qualtrics IDs per fiscal year_*
SQL query:

    select FISCAL_YEAR,
    count(distinct qualtrics_id) as total_qualtrics_id
    from "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY"
    where EBA_FLAG = 'FALSE'
    group by 1

### Non-EBA Qualtrics IDs per Fiscal Year

| FISCAL_YEAR | total_qualtrics_id |
| ------ | ------ |
| 2023 | 100 |
| 2022 | 80 |
| 2021 | 50 |
| 2020 | 35 |

![Total_Qualtrics_ID vs Fiscal_Year](https://res.cloudinary.com/dffvrw1wk/image/upload/v1690742152/002_fgcmpv.jpg)

#### Table Summary
The query helps identify the number of survey responses (Qualtrics IDs) submitted by non-EBA participants for each fiscal year. It focuses on data from a specific table and filters out only the relevant responses before grouping them by fiscal year for analysis. 

#### Table Results
The total number of survey responses (Qualtrics IDs) have increased year on year since 2020 from 35 to over 100 responses in 2023.

## 5.2 Use Case 2
### *To fetch Qualtrics IDs (EBA and non-EBA) per industry*
SQL query:

    SELECT INDUSTRY,
    COUNT(DISTINCT QUALTRICS_ID),
    COUNT(DISTINCT account_csn)
    from "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY"
    GROUP BY INDUSTRY;

| INDUSTRY | total_qualtrics_id | total_account_csn |
| ------ | ------ | ------ |
| UNKNOWN | 1850 | 3700 |
| CONSTRUCTION | 1500 | 3000 |
| ARCHITECTURE | 1250 | 1500 |
| PRODUCT DESIGN | 900 | 1800 |


![Total_Qualtrics_ID vs Fiscal_Year](https://res.cloudinary.com/dffvrw1wk/image/upload/v1690742564/003_gnaube.jpg)

#### Table Summary
The query helps identify the number of survey responses (Qualtrics IDs) and the number of unique customers (account_csn) for both EBA and non-EBA participants, categorized by different industries. It allows us to understand how many survey responses and unique customers are associated with each industry.

#### Table Results
Engagement and feedback vary by industry. The majority of respondents are unique customers with an unknown industry. Investigate to identify these industries. Improve survey participation and engagement, especially in construction and product design industries.

## 5.3 Use Case 3
### *To fetch EBA Qualtrics IDs per GEO*
SQL query:

    with count_rows as
    (select count(distinct qualtrics_id) as qualtrics_count
    from
    "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY" )
    --where powerbi_geo = ''_)
    ,total_promoters as (
    Select count(distinct qualtrics_id) as promoters_count from
    "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY" where score >='9')
    ,total_detractors as (
    Select count(distinct qualtrics_id) as detractors_count from
    "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY" where score <='6')
    select promoters_perc - detractors_perc
    from (
    select promoters_count/qualtrics_count as promoters_perc, detractors_count/qualtrics_count as detractors_perc
    from count_rows,total_promoters,total_detractors
    )

| GEO | Total EBA Qualtrics IDs | Promoters Count | Detractors Count | NPS (Promoters - Detractors) |
| ------ | ------ | ------ | ------ | ------ |
| Geo_1 | 1200 | 800 | 150 | 650 |
| Geo_2 | 850 | 400 | 70 | 330 |
| Geo_3 | 500 | 250 | 50 | 200 |






#### Table Summary

- "GEO" represents the geographic location categories for which the NPS is calculated.
- "Total EBA Qualtrics IDs" shows the total count of EBA Qualtrics survey responses for each geographic location.
- "Promoters Count" displays the count of Promoters (survey responses with a score of 9 or 10) in each GEO.
- "Detractors Count" shows the count of Detractors (survey responses with a score of 0 to 6) in each GEO.
- "NPS (Promoters - Detractors)" calculates the Net Promoter Score for each GEO by subtracting the percentage of Detractors from the percentage of Promoters.

Each row in the table represents a different GEO category, and the corresponding columns contain the relevant information for that category. This tabular representation facilitates easy comparison of NPS values across different geographic locations, allowing for identification of regions with higher or lower levels of customer sentiment and loyalty.
#### Table Results
-   Geo_1 has 1200 EBA Qualtrics survey responses, with 800 promoters and 150 detractors, resulting in an NPS of 650.
-   Geo_2 has 850 EBA Qualtrics survey responses, with 400 promoters and 70 detractors, resulting in an NPS of 330.
-   Geo_3 has 500 EBA Qualtrics survey responses, with 250 promoters and 50 detractors, resulting in an NPS of 200.

Overall, Geo_1 has the highest NPS, indicating a higher level of customer loyalty and satisfaction compared to the other locations. Geo_3 has the lowest NPS, suggesting there is room for improvement in customer sentiment in this area.


## 5.4 Use Case 4
### *To calculate overall NPS (EBA and non-EBA)*
SQL query:

    with count_rows as
    (select count(distinct qualtrics_id) as qualtrics_count
    from
    "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY" )
    ,total_promoters as (
    Select count(distinct qualtrics_id) as promoters_count from
    "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY" where score >='9')
    ,total_detractors as (
    Select count(distinct qualtrics_id) as detractors_count from
    "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY" where score <='6')
    select promoters_perc - detractors_perc as overall_nps
    from (
    select promoters_count/qualtrics_count as promoters_perc, detractors_count/qualtrics_count as detractors_perc
    from count_rows,total_promoters,total_detractors
    )

| Overall NPS | 
| ------ |
| 35 |

#### Table Summary

- "Overall NPS" represents the calculated Net Promoter Score for both EBA (Employee-Based Access) and non-EBA Qualtrics survey responses combined.
- The table contains a single row, and the value "35" indicates the overall Net Promoter Score resulting from the analysis.
- The overall NPS is derived by subtracting the percentage of Detractors from the percentage of Promoters, considering both EBA and non-EBA responses.
- This score provides an assessment of the overall sentiment and loyalty of all survey participants across the entire dataset.
#### Table result
An NPS (Net Promoter Score) of 35 means that the overall sentiment of customers towards a company, product, or service is positive but has room for improvement. The NPS is measured on a scale from -100 to +100. It shows that there are more promoters than detractors, but there is still room for improvement to further increase customer satisfaction and loyalty.

## 5.5 Use Case 5
### *To calculate EBA NPS*
SQL query:

    with count_rows as
    (select count(distinct qualtrics_id) as qualtrics_count
    from
    "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY" where EBA_FLAG = 'TRUE')
    ,total_promoters as (
    Select count(distinct qualtrics_id) as promoters_count from
    "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY"
    where score >='9' AND EBA_FLAG = 'TRUE')
    ,total_detractors as (
    Select count(distinct qualtrics_id) as detractors_count from
    "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY"
    where score <='6' AND EBA_FLAG = 'TRUE')
    select promoters_perc - detractors_perc as overall_eba_nps
    from (
    select promoters_count/qualtrics_count as promoters_perc, detractors_count/qualtrics_count as detractors_perc
    from count_rows,total_promoters,total_detractors
    )

| Overall EBA NPS | 
| ------ |
| 60 |
#### Table Summary

- "Overall EBA NPS" represents the calculated Net Promoter Score for EBA (Employee-Based Access) Qualtrics survey responses.
- The table contains a single row, and the value "60" indicates the EBA-specific Net Promoter Score resulting from the analysis.
- The EBA NPS is derived by subtracting the percentage of Detractors from the percentage of Promoters, considering only EBA responses.
- This score provides an assessment of customer sentiment and loyalty specifically for Employee-Based Access survey participants.
#### Table results
- An overall EBA (Employee-Based Access) NPS (Net Promoter Score) of 60 means that the sentiment of employees who have access to a company's products or services is highly positive. 
- It indicates that a significant majority of employees who have access to the company's products or services are promoters. This suggests a high level of employee satisfaction and loyalty, which is beneficial for the company as it indicates a positive work environment and can lead to higher employee engagement and productivity.

## 5.6 Use Case 6
### *To connect NPS table with applicable dimensions*
SQL query:

    WITH ACCOUNT_CED AS (
    SELECT
    -- site location identifying information
    t_map.account_csn as ACCOUNT_CSN
    ,SITE_TYPE
    ,SITE_COUNTRY_NAME
    ,SITE_GEO
    ,SITE_INDUSTRY_SEGMENT
    ,SITE_INDUSTRY_GROUP
    ,PARTNER_SITE_TYPE
    ,SITE_SALES_REGION
    ,SITE_TYPE
    ,SITE_NAMED_ACCOUNT_GROUP_STATIC
    ,CORPORATE_CUSTOMER_SIZE_STATIC
    from adp_publish.account_optimized.account_edp_optimized account_ced
    inner join adp_publish.account_optimized.transactional_csn_mapping_optimized t_map
    on t_map.site_uuid_csn = account_ced.site_uuid_csn
    )
    SELECT SCORE, ACCOUNT_CED.*
    "EIO_PUBLISH"."ENGAGEMENT_SHARED"."NPS_EBA_NON_EBA_SURVEY" SURVEY
    LEFT JOIN ACCOUNT_CED ON
    SURVEY.ACCOUNT_CSN = ACCOUNT_CED.ACCOUNT_CSN

| SCORE | ACCOUNT_CSN | SITE_TYPE | SITE_COUNTRY_NAME | SITE_GEO | SITE_INDUSTRY_SEGMENT | SITE_INDUSTRY_GROUP |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 9 | CSN_001 | Type_A | Country_X | Geo_1 | Segment_1 | Group_A |
| 7 | CSN_002 | Type_B | Country_Y | Geo_2 | Segment_2 | Group_B |
| 8 | CSN_003 | Type_C | Country_Z | Geo_3 | Segment_3 | Group_C |

#### Table Summary

- "SCORE" represents the Net Promoter Score for each survey response.
- "ACCOUNT_CSN" is the customer account identifier that connects the NPS survey responses to specific customers in the "ACCOUNT_CED" result set.
- Other columns like "SITE_TYPE," "SITE_COUNTRY_NAME," "SITE_GEO," "SITE_INDUSTRY_SEGMENT," "SITE_INDUSTRY_GROUP," and more represent site location and customer attributes from the "ACCOUNT_CED" result set.
- The table combines NPS data with relevant dimensions from "ACCOUNT_CED" using a LEFT JOIN. This links each NPS survey response to its corresponding customer and includes additional information about site location and industry segment.

#### Table Result
We can leverage NPS tables to facilitate in-depth analysis by exploring NPS scores alongside specific customer attributes, gaining insights into customer feedback and loyalty based on different dimensions.

## 6. Report / Data for Reconciliation
- Sales Transactions
- Software Modules
- Software Product Updates
- Software Product Usage
- Software Product Integration
- Customer support tickets


## 7. Metric Owner Check List
| ID | Item | Comments |
| ------ | ------ | ------ |
| 1 | Is the metric defined and used consistently across ADSK? | Based on the fact of having multiple SME's for this metric, this needs to be checked and agreed upon for a standardised approach going forward  |
| 2 | Has this metric been signed off and approved by identified stakeholders? | Yes, the metric has been reviewed and approved by relevant stakeholders to ensure its accuracy and appropriateness for decision-making. |
| 3 | Has the metric gone through spot checks, checks for edge cases, and peer-level review? | Yes, the metric has undergone spot checks, edge case analysis, and review by peers to verify its accuracy and reliability.  |
| 4 | Is all logic defined and stored outside of a dashboard? | Yes, the logic and calculations for the metric are documented and stored separately from the dashboard to ensure consistency and maintainability.  |
| 5 | Is the metric accessible and available in ADP-Hive (where applicable)? | Yes, the metric is accessible and available in ADP-Hive for relevant teams to access and analyze the data. |
| 6 | Is the metric accessible and available in ADP Snowflake (where applicable)? | Yes, the metric is accessible and available in ADP Snowflake for relevant teams to access and analyze the data. |
| 7 | Do you have a process for proactively communicating changes and known issues? |Yes, there is a process in place to proactively communicate any changes to the metric's definition or data sources, as well as any known issues that may impact its accuracy or availability.  |
| 8 | Have you considered impacts to external parties such as partners/customers? | Yes, potential impacts on external parties, including partners and customers, have been taken into account to ensure that the metric's results are relevant and reliable for all stakeholders. |

## 8. Governance
This is for any version updates to how the metric is defined.
| Version | Start date | End date | Description of Change/Update | Comments |
| ------ | ------ | ------ | ------ | ------ |
| 1.0 | 06 Feb 2023 | 30 July 2023 | Metric documentation available through KPI Simplification Initiative.| This metric was available prior to this start date, but the date reflects when this logic documentation was created for KPI Simplification.|
| 2.0| 31 July 2023 | - | Introduced robust workflow for metric calculation. | Updated how the metric is calculated to enhance the accuracy of the NPS metric.
# 9. Data Quality & Monitoring
## 10. Known Data Quality Issues
1. Not all Qualtrics_id have an account_csn, hence not all qualtrics_id will have an account_name
2. For ADSK_BUSINESS_SCORE the NPS threshold is unusual, it's FY21_ADSK_BUSINESS_SCORE >= 6 THEN 'PROMOTER' WHEN
FY21_ADSK_BUSINESS_SCORE <= 3 THEN 'DETRACTOR' for all others when SCORE <= 3 then Detractor and
SCORE >= 9 then Promoter
3. As of 31/07/2023, About 1850 qualtrics_id have multiple ACCOUNT_CSN mapped to them, some of these CSN's have either have multiple ACCOUNT_NAME, INDUSTRY & GEO or multiple values in one of these filters, so in order to ensure consistency, any qualtrics_id with multiple ACCOUNT_CSN will have ACCOUNT_NAME, INDUSTRY and GEO set to 'UNKNOWN'
## 10.1 Data Quality Checks
- Unique fields
    - QUALTRICS_ID
- Not null fields:
    - QUALTRICS_ID
    -  CURRENT_FY_FLAG
    - DT
    - EBA_FLAG

• Accepted value testing:
| Fields | Max Value | Min Value |
| ------ | ------ | ------ |
| ACCOUNT_TEAMS_SCORE | 11 | 0 |
| ADSK_ABILITY_PROD_LIC_SCORE | 11 | 0 |
| ADSK_BUSINESS_SCORE | 9 | 0 |
| ADSK_INTEGRITY_SCORE | 11 | 0 |
| HIGH_QUALITY_PRODUCT_SCORE | 11 | 0 |
| PROD_SVC_COMPARED_SCORE | 11 | 0 |
| PROD_SVC_SCORE | 11 | 0 |
| SME_ACCESS_SCORE | 11 | 0 |
| SCORE | 11 | 0 |

## 10.2 Inventory of Downstream Users
| Report / Process Title | Report / Process Description | Link to More Details | Consumers |
| ------ | ------ | ------ | ------ |
| NPS dashboard | This is a tool to check how likely customers are on recommending Autodesk, or in other words, how happy they are with Autodesk at the moment or historically depending on the amount of replied surveys. | [Link](https://www.autodesk.eu/) | CSM (Customer Success Management) team & SP (Sales and Product) organizations |
| Sales Performance Report | This report provides insights into the sales performance of Autodesk products. It includes information on sales revenue, trends, and key performance indicators. | [Link](https://www.autodesk.eu/) | Sales and Marketing teams |
| Product Usage | This system tracks and manages Autodesk's module usage, including license levels, license availability, and orders. It helps optimize license control and ensures efficient supply chain management. | [Link](https://www.autodesk.eu/) | Supply Chain and Operations teams | 
| Customer Support Tickets | This report analyzes customer support tickets to identify common issues and trends. It helps improve customer service and product enhancements based on customer feedback and pain points. | [Link](https://www.autodesk.eu/) | Customer Support and Product Development teams |
| Governance | This is for any version updates to how the metric is defined. | [Link](https://www.autodesk.eu/) | Metrics Team and Governance Committee |

[![Build Status](https://brand.autodesk.com/app/uploads/2021/04/primary-logo-1.svg)](https://travis-ci.org/joemccann/dillinger)