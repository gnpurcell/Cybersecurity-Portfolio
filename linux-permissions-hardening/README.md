# Linux File Permissions Hardening

## **Overview**
Audited and hardened file and directory permissions in a Linux environment to enforce least privilege and protect sensitive project data. :contentReference[oaicite:2]{index=2}  

## **Objective**
Identify misconfigurations in file permissions, correct them using `chmod`, and ensure only authorized users can access or modify sensitive files.

## **Tools Used**
- Linux terminal
- `pwd`, `cd`
- `ls`, `ls -l`, `ls -la`
- `chmod`

## **Tactics / Techniques**
- Endpoint / host hardening  
- Least privilege enforcement  
- Hidden file discovery and remediation

## **Findings**
- Files in the `projects` directory had **overly permissive write access** for group/other.  
- A hidden archived file, `.project_x.txt`, was writable when it should have been read-only.  
- The `drafts` directory permissions allowed unnecessary group access to sensitive content.

## **Actions Taken**
- Used `ls -l` and `ls -la` to inspect permissions on all visible and hidden files.  
- Removed write permissions from group/other on sensitive files like `project_m.txt`.  
- Modified `.project_x.txt` so that it is **read-only** for user and group.  
- Restricted directory permissions on `drafts` so only the **researcher2** user can access it.

## **Impact**
- Reduced risk of accidental or malicious modification of sensitive research files.  
- Minimized exposure of hidden/archived files.  
- Improved alignment with least privilege and secure file system practices.

## **Key Commands Used**
- `pwd` – confirm working directory  
- `cd` – navigate between directories  
- `ls`, `ls -l`, `ls -la` – list files and permissions  
- `chmod` – modify permissions (e.g. `u-w`, `g-w`, `g+r`, `g-x`, `o-w`)

## **Key Skills Demonstrated**
- Linux command-line proficiency  
- File system auditing and hardening  
- Practical least privilege implementation  
- Endpoint security fundamentals
