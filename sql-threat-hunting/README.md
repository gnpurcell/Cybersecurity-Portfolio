# SQL Threat Hunting & Login Investigation

## **Overview**
Used SQL to investigate employee login activity and identify abnormal behavior that could indicate compromised accounts or misuse of credentials.
## **Objective**
Detect suspicious login patterns such as after-hours access, logins from unusual locations, and activity around a specific incident date.

## **Tools Used**
- SQL
- Authentication / login logs
- Filtering operators (AND, OR, NOT, LIKE)

## **Tactics / Techniques**
- Behavioral analysis of user logins  
- Detection of potential credential misuse  
- Identification of anomalous access patterns

## **Findings**
- Multiple **failed login attempts after 18:00 (6 PM)**, increasing likelihood of password guessing or brute force attempts.  
- Login attempts originating from **outside Mexico**, identified using `NOT LIKE 'MEX%'`.  
- Activity clustered around a specific incident window by querying **incident date and the day before**.  
- Department-based queries highlighted which teams (e.g., Marketing, Finance, Sales) would be impacted by targeted security changes.

## **Impact**
- Increased risk of account compromise if abnormal login patterns go undetected.  
- Potential for unauthorized access from foreign locations.  
- Lack of visibility into department-level access behavior could delay incident detection.

## **Recommendations**
- Enforce **MFA** for all users.  
- Create alerts for:
  - **After-hours failed logins**
  - **Logins from non-approved countries**
  - **Spikes in failed attempts per user/device**
- Apply **least privilege** and department-based access controls.  
- Regularly review authentication logs using structured SQL queries.

## **Key Skills Demonstrated**
- Threat hunting with SQL  
- Log/data analysis for security  
- Pattern recognition and anomaly detection  
- Translating query results into security actions
