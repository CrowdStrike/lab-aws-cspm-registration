![](https://raw.githubusercontent.com/CrowdStrike/falconpy/main/docs/asset/cs-logo.png)

# Cloud Security Lab Series
## AWS CSPM Registration 101

### Requirements
One or more of these subscriptions:
- Falcon Cloud Security
- Falcon Cloud Security with Containers

One or more of these default roles:
- Falcon Administrator
- Cloud Security Manager
- CSPM Manager
- CSPM Misconfiguration Manager

### Prerequisites
CrowdStrike API Client ID and Secret with the `CSPM REGISTRATION` scope and `Read` and `Write` permissions enabled. 
For more info, see [API clients](https://falcon.crowdstrike.com/documentation/page/a2a7fc0e/crowdstrike-oauth2-based-apis#mf8226da).

**Note**: A CSPM Admin or CSPM Analyst must obtain the API credentials from a Falcon Administrator to successfully register a cloud account.

### Table of Contents
- [Chapter 1 - What is AWS CSPM Registration?](guide/chapter1.md)
- [Chapter 2 - Using the cspm-registration API](guide/chapter2.md)
- [Chapter 3 - Guided Registration via Falcon Console](guide/chapter3.md)
- [Chapter 4 - Using a Custom template](guide/chapter4.md)
- [Chapter 5 - Using a Custom Template for GovCloud Falcon](guide/chapter5.md)
- [Chapter 6 - CSPM Architecture](guide/chapter6.md)
- [Chapter 7 - Organization Registration](guide/chapter7.md)
- [Chapter 8 - Multiple Account Registration](guide/chapter8.md)
- [Chapter 9 - Cleanup](guide/chapter9.md)

### Questions or concerns?
If you encounter any issues or have questions about this repository, please open an [issue]().