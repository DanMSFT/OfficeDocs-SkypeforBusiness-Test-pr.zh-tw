﻿---
title: 'Lync Server 2013: Testing messaging using XMPP'
TOCTitle: Testing messaging using XMPP
ms:assetid: ae5305ba-e5fc-4ca0-a805-872b4ebaf981
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn727312(v=OCS.15)
ms:contentKeyID: 62388509
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Testing messaging using XMPP in Lync Server 2013

 

_**上次修改主題的時間：** 2015-03-09_


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Verification schedule</p></td>
<td><p>Daily</p></td>
</tr>
<tr class="even">
<td><p>Testing tool</p></td>
<td><p>Windows PowerShell</p></td>
</tr>
<tr class="odd">
<td><p>Permissions required</p></td>
<td><p>When run locally using the Lync Server 管理命令介面, users must be members of the RTCUniversalServerAdmins security group.</p>
<p>When run using a remote instance of Windows PowerShell, users must be assigned an RBAC role that has permission to run the <strong>Test-CsXmppIM</strong> cmdlet. To see a list of all RBAC roles that can use this cmdlet, run the following command from the Windows PowerShell prompt:</p>
<pre><code>Get-CsAdminRole | Where-Object {$_.Cmdlets -match &quot;Test-CsXmppIM&quot;}</code></pre></td>
</tr>
</tbody>
</table>


## Description

The Extensible Messaging and Presence Protocol (XMPP) is a standard communications protocol (based on XML) used for sending messages across the Internet. XMPP was originally named Jabber, and is supported by several Internet messaging and communication applications, such as Google Talk and Facebook Chat. The **Test-CsXmppIM** cmdlet verifies that a user can exchange instant messages with a user on an XMPP network. Note that, for this test to succeed, you must have a valid SIP address for the XMPP user, and that SIP address must be on a network that was configured as an allowed XMPP partner.

## Running the test

The following example verifies the XMPP instant messaging capabilities for the pool atl-cs-001.litwareinc.com. This command will work only if test users are defined for the pool atl-cs-001.litwareinc.com. If they have, then the command will determine whether the first test user can send an XMPP instant message to a user who has the SIP address adelaney@contoso.com.

If test users are not defined, then the command will fail because it won't know which user to log on as. If you have not defined test users for a pool, then you must include the UserSipAddress parameter and the credentials of the user who the command should use when trying to log on.

    Test-CsXmppIM -TargetFqdn "atl-cs-001.litwareinc.com" -Receiver "adelany@contoso.com"

The commands shown in the next example test the ability of a specific user (litwareinc\\pilar) to log on to send an XMPP instant message to the user adelaney@contoso.com. To do this, the first command in the example uses the Get-Credential cmdlet to create a Windows PowerShell command-line interface credential object that contains the name and password of the user Pilar Ackerman. (Because the logon name litwareinc\\pilar was included as a parameter, the Windows PowerShell Credential Request dialog box only requires the administrator to enter the password for the Pilar Ackerman account.) The resulting credential object is then stored in a variable named $cred1.

The second command then checks whether this user can log on to the pool atl-cs-001.litwareinc.com and send the XMPP instant message. To run this task, the **Test-CsXmppIm** cmdlet is called, together with four parameters: TargetFqdn (the FQDN of the Registrar pool); Receiver (the SIP address of the user the message is being addressed to); UserCredential (the Windows PowerShell object that contains Pilar Ackerman’s user credentials); and UserSipAddress (the SIP address that corresponds to the supplied user credentials).

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsXmppIM -TargetFqdn "atl-cs-001.litwareinc.com" -Receiver "adelany@contoso.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

## Determining success or failure

If XMPP instant messaging is correctly configured, you'll receive output similar to this, with the Result property marked as **Success:**

Target Fqdn : atl-cs-001.litwareinc.com

Result : Success

Latency : 00:00:02.5361946

Error Message :

Diagnosis :

If the specified users can't use XMPP instant messaging, the Result will be shown as **Failure**, and additional information will be recorded in the Error and Diagnosis properties:

WARNING: Failed to read Registrar port number for the given fully qualified

domain name (FQDN). Using default Registrar port number. Exception:

System.InvalidOperationException: No matching cluster found in topology.

at

Microsoft.Rtc.Management.SyntheticTransactions.SipSyntheticTransaction.TryRetri

eveRegistrarPortFromTopology(Int32& registrarPortNumber)

Target Fqdn : atl-cs-001.litwareinc.com

Result : Failure

Latency : 00:00:00

Error Message : 10060, A connection attempt failed because the connected party

did not properly respond after a period of time, or

established connection failed because connected host has

failed to respond 10.188.116.96:5061

Inner Exception:A connection attempt failed because the

connected party did not properly respond after a period of

time, or established connection failed because connected host

has failed to respond 10.188.116.96:5061

Diagnosis :

## Reasons why the test might have failed

Here are some common reasons why **Test-CsXmppIM** might fail:

  - An incorrect parameter value was supplied. If used, the optional parameters must be configured correctly or the test will fail. Rerun the command without the optional parameters and see whether that succeeds.

  - This command will fail if XMPP gateway configuration is misconfigured or not yet deployed.

## 請參閱

#### 其他資源

[Set-CsXmppGatewayConfiguration](set-csxmppgatewayconfiguration.md)

