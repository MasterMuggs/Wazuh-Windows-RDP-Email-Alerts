# Wazuh-Windows-RDP-Email-Alerts
Custom Local-Rules for Wazuh to email when an RDP session is initiated


To get the alerts to work you need to modify the Wazuh Rules 
1) Open Wazuh Dashboard > Rules > Custom Rules
![image](https://github.com/user-attachments/assets/817ef5dc-0eda-42bc-a103-accd381f7b94)
2) Click on "Add new rules file"
3) Copy and Paste the code from the local_rules.xml
4) Save


You will also need to modify the OSSEC file on the endpoints, if these are not already enabled make sure to include the following if you want to be alerted via email for the new rule.

This snippet will ensure your email alerts are setup. (This snippet is just an example of the fields which need to be enabled already)
```XML
<ossec_config>
  <global>
    <email_notification>yes</email_notification>
    <smtp_server>smtprelay.emailprovider.com</smtp_server>
    <email_from>wazuh@emailprovider.com</email_from>
    <email_to>wazuhalerts@emailprovider.com</email_to>
  </global>
```
The alert email level below has to be set at or lower than the level set on the local_ruleset.xml file.
```XML
  <alerts>
    <log_alert_level>3</log_alert_level>
    <email_alert_level>10</email_alert_level>
  </alerts>
```
This ensures that the email will be sent out for the RDP Windows Ruleset.
```XML
  <email_alerts>
  <email_to>wazuhalerts@emailprovider.com</email_to>
  <rule_id>60106</rule_id>
  <do_not_delay />
  </email_alerts> 

```
