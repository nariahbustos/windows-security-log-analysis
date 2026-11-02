# Windows Security Log Analysis
## 1. Investigation Objective
Review Windows Security and System event logs to identify failed authentication attempts, successful logons, and potentially suspicious service activity.

## 2. Evidence Collected
### Failed Logons — Event ID 4625

- Identified two failed interactive logon events.
- Both events used Logon Type 2.
- Both involved the same account.
- One failure reported "unknown user or bad password."
- The second included status 0xC000006D and substatus 0xC0000380, consistent with a smart-card-related incorrect PIN.

### Successful Logon — Event ID 4624
- Identified a successful service logon.
- Logon Type: 5.
- Account: SYSTEM.
- Process: C:\Windows\System32\services.exe.
- Elevated Token: Yes.
- A Logon ID was identified.

### Special Privileges — Event ID 4672
- Found an event matching the successful logon's Logon ID.
- This indicates special privileges were assigned to the SYSTEM logon session.

### Service Installation — Event ID 7045
- Identified service: EasyAntiCheat_EOSSys.
- File path: C:\Program Files (x86)\EasyAntiCheat_EOS\EasyAntiCheat_EOS.sys.
- The event occurred close in time to the successful service logon.
- The service is associated with Easy Anti-Cheat, a legitimate gaming anti-cheat component.

### Service Activity — Event ID 7036
No matching service start/stop event was identified during the review.

## 3. Analysis
The successful Type 5 logon was associated with the Windows Service Control Manager and the SYSTEM account. The matching Event ID 4672 supports that the session received elevated privileges.
The Event ID 7045 record identified Easy Anti-Cheat as the installed service. Its identity and timing provide a plausible legitimate explanation for the service-related activity.
The two failed interactive logons were separate authentication events. The available evidence does not establish that they were caused by Easy Anti-Cheat or that they were connected to the successful service logon.

## 4. Conclusion
The reviewed logs show two failed interactive authentication attempts and a successful privileged SYSTEM service logon.
The service installation was identified as Easy Anti-Cheat, which provides a plausible legitimate explanation for the related service activity.
Based on the available evidence, there is insufficient support to conclude that unauthorized access or malicious activity occurred. The relationship between the failed interactive logons and the service activity remains unconfirmed.

## 5. Skills Demonstrated
- Windows Event Viewer
- Windows Security Log Analysis
- Authentication Event Investigation
- Event ID 4624, 4625, 4672, 7036, and 7045 analysis
- Logon Type interpretation
- Windows service investigation
- Evidence-based incident documentation
