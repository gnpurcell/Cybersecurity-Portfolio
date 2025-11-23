# Impossible Travel Alert Investigation  
**Tool:** Splunk Enterprise Security  
**Alert Type:** Authentication Anomaly  
**SOC Severity:** Medium  
**Investigation Status:** Closed – Confirmed Suspicious  
**MITRE Techniques:**  
- T1078 – Valid Accounts  
- T1110 – Credential Abuse  
- T1059 – Command Execution (Potential Follow-Up)

---

## **Overview**
Splunk generated an **Impossible Travel alert** for user **j.doe@company.com** after two successful logins occurred from geographically impossible locations within a short timeframe.  
This type of alert typically indicates **credential compromise** or use of **stolen session tokens**.

---

## **Objective**
Determine whether the activity is:
- A legitimate user traveling  
- A VPN or geo-location anomaly  
- Or a compromised account being accessed from multiple regions

---

## **Tools Used**
- Splunk Search Processing Language (SPL)  
- Enterprise Security Authentication Data Model  
- GeoIP lookup  
- Risk Analysis Framework  

---

# SPLUNK QUERIES USED

## **1️⃣ Pull Authentication Events for the User**

```spl
index=authentication user="j.doe" action="success"
| table _time user src_ip city country app
| sort _time
```
## **2️⃣ Enrich with GeoIP & Calculate Speed Between Logins**
```spl
index=authentication user="j.doe" action="success"
| iplocation src_ip
| sort _time
| streamstats current=f last(latitude) as last_lat last(longitude) as last_long last(_time) as last_time
| eval distance_km = haversine(latitude, longitude, last_lat, last_long)
| eval time_diff = _time - last_time
| eval travel_speed_kph = round(distance_km / (time_diff/3600), 2)
| table _time user src_ip city country distance_km time_diff travel_speed_kph
```
## **3️⃣ Check for Failed Login Attempts Before or After**
```spl
index=authentication user="j.doe" action="failure"
| stats count by src_ip, city, country
```
## **4️⃣ Check for Lateral Movement Indicators**
```spl
index=endpoint user="j.doe" (process_name=cmd.exe OR process_name=powershell.exe)
| table _time host process_name command_line
```

**Findings** 
1. Suspicious Login Pattern

Two successful logins occurred:

Time (UTC)    City      Country         IP
08:14         Denver    United States   72.xxx.xx.14
08:27         Warsaw    Poland          185.xxx.xx.91

Distance: 8,729 km  
Time between logins: 13 minutes  
Travel Speed Required: 40,320 km/h (physically impossible for a human)

➤ Conclusion: Impossible travel confirmed.

2. Pre-Attack Failed Logins
Multiple failed attempts from Polish IP ranges were observed 3 hours before the successful login.  
This suggests password spraying or brute

3. Post-Login Activity
A quick check showed no suspicious endpoint commands, meaning the attacker likely logged in but did not yet execute anything major.  
However, email access was logged, indicating the attacker may have simply been browsing the mailbox.

**SOC Determination**

Status: **Confirmed suspicious**  
Reason: Strong indicators of compromised credentials.

Evidence:
- Successful login from foreign IP never previously associated with the user  
- Failed login attempts from same country shortly before  
- Impossible travel speed  
- No VPN usage confirmed by IT  
- User confirmed they were *not* in Poland  
