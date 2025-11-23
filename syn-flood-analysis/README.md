# SYN Flood Attack Analysis

## **Overview**
Investigated abnormal network traffic causing site outages. Identified a **SYN flood attack** overwhelming server resources via excessive half-open TCP connections.

## **Objective**
Determine the root cause of the service interruption and analyze attacker behavior using log data.

## **Tools Used**
- Log files  
- TCP/IP analysis  
- Linux CLI  

## **Tactics / Techniques**
- **DoS (SYN Flood)**  
- Abuse of the **TCP three-way handshake**  
- **Resource exhaustion**

## **Findings**
- High volume of SYN packets originating from **203.0.113.0**  
- Server entered half-open connection overload  
- Logs show saturation beginning at **entry 52** and total failure by **entry 98**

## **Impact**
- Legitimate users received timeout errors  
- Server unable to allocate resources for valid TCP connections  
- Service disruption across the web environment

## **Recommendations**
- Enable **SYN cookies**  
- Apply **rate limiting** + firewall rules  
- Add **IDS/IPS detection** for SYN flood patterns  
- Harden perimeter devices against volumetric DoS attacks  

## **Key Skills Demonstrated**
- Log analysis  
- TCP fundamentals  
- DoS identification  
- SOC-style incident triage
