# Data Leak Analysis & Least Privilege Review

## **Overview**
Analyzed a data leak involving internal-only product documents that were accidentally exposed externally due to excessive access and link sharing.
## **Objective**
Identify how the data leak occurred, map it to least privilege failures, and recommend controls aligned with NIST SP 800-53 AC-6.

## **Incident Summary**
- A sales manager shared access to a folder containing **internal product files**, customer analytics, and promotional materials with their team.  
- Access was **not revoked** after the meeting.  
- A sales rep later shared the **entire folder link** with a business partner, intending only to share promotional assets.  
- The business partner posted the link publicly on social media, unintentionally exposing internal documents.

## **Root Cause**
- Excessive access granted beyond what was required for the task.  
- No automatic expiration or revocation of access after the meeting.  
- Lack of strong access controls and oversight around sensitive folders.

## **Control Reference – NIST SP 800-53 AC-6 (Least Privilege)**
- Users should receive only the **minimal access** needed to complete their tasks.  
- Processes, user accounts, and roles must enforce least privilege to prevent excessive permissions.  
- Enhancements include:
  - Restrict access based on **user role**  
  - Automatically **revoke access** after a period of time  
  - Maintain **activity logs** for provisioned accounts  
  - Regularly **audit user privileges**

## **Recommendations**
- Automatically **expire shared folder access** after a defined time window.  
- Implement **role-based access control (RBAC)** for sensitive internal resources.  
- Maintain detailed **access logs** and regularly audit them.  
- Provide training to staff on secure sharing practices and classification of internal vs. external assets.

## **Impact**
- Exposure of unreleased product information.  
- Potential reputational harm and competitive disadvantage.  
- Weak enforcement of access control policies.

## **Key Skills Demonstrated**
- Incident analysis and root-cause identification  
- Application of NIST SP 800-53 (AC-6: Least Privilege)  
- Governance, risk, and compliance thinking  
- Designing practical access control improvements
