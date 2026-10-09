# Roadmap

## ✅ Completed

- [x] Deploy Wazuh all-in-one on Rocky Linux (VMware)
- [x] Enroll Windows 10 agent
- [x] Install and configure Sysmon
- [x] Forward Sysmon event channel to Wazuh
- [x] Configure real-time File Integrity Monitoring
- [x] Review CIS SCA results

## 🔜 Next Up

### VirusTotal Integration
- [ ] Create a VirusTotal API key (free tier)
- [ ] Add the `<integration>` block to the manager's `ossec.conf`
- [ ] Trigger on FIM events (`syscheck` group)
- [ ] Test with the EICAR test file
- [ ] Document the alert flow and API rate limits

### Active Response
- [ ] Configure a command and active-response block on the manager
- [ ] Auto-remove files flagged malicious by VirusTotal
- [ ] Verify via `active-responses.log` on the agent
- [ ] Document risks (false positives) and rollback

### Suricata (Network IDS)
- [ ] Deploy Suricata on [Linux sensor VM]
- [ ] Install a Wazuh agent on the sensor
- [ ] Ingest `eve.json` into Wazuh
- [ ] Generate test traffic (e.g. port scan with nmap) and verify alerts

### EVE-NG Network Lab
- [ ] Build a multi-device topology
- [ ] Connect monitored hosts to Wazuh
- [ ] Simulate attacks across segments

## 💡 Ideas Backlog

- [ ] Harden Windows 10 and re-run the CIS benchmark to show score improvement
- [ ] Add a Linux endpoint agent
- [ ] Write custom Wazuh rules and decoders
- [ ] Simulate attacks (Atomic Red Team) and map detections to MITRE ATT&CK
- [ ] Build custom dashboards and saved searches
- [ ] Email or Slack alerting
- [ ] Vulnerability Detection module walkthrough