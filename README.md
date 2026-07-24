# AI-SOC
Automatically triages a Splunk security alert, extracts and enriches indicators of compromise (IPs, domains, hashes), runs threat-intel lookups (VirusTotal, AbuseIPDB), and generates a clear, actionable investigation report — optionally sent as an HTML email to your SOC or on-call inbox.
Provide a Splunk alert JSON (paste into the alert_data field) or send alerts to the /webhook endpoint.
Set a recipient email to receive the HTML incident report (or configure SOC_RECIPIENT_EMAIL as an env var).
Ensure the deployment has:
A configured CodeWords runtime / API key (for Composio tools).
Access to threat-intel tools (VirusTotal, AbuseIPDB) via the runtime.
A configured Gmail send tool (for email delivery).
Optional: adjust how many IOCs to enrich (defaults are built into the workflow).
Receives a raw Splunk alert (manual POST or webhook).
Uses an LLM to perform an initial triage (severity, alert type, confidence, 1–2 sentence summary).
Runs regex-based IOC extraction (IPs, domains, URLs, file hashes) and then asks an LLM to extract any additional IOCs the regex missed.
Performs parallel threat-intel enrichment (VirusTotal for IPs/domains/hashes and AbuseIPDB for IP reputations) via Composio tools.
Uses a senior-analyst LLM prompt to produce a structured investigation report: executive summary, IOC table, threat-intel summary, MITRE ATT&CK mapping, risk assessment, and recommended actions.
Builds a polished HTML email with severity styling and sends it via the configured Gmail tool (if recipient set).
Returns a JSON analysis response summarizing results (severity, IOC counts, enrichment queries, and full report).
A concise, SOC-ready HTML incident report containing:
Executive summary and severity label.
IOC table (type, value, quick intel summary).
Threat-intel highlights and enrichment details.
MITRE ATT&CK techniques mapped to the incident.
Risk assessment and prioritized recommended actions.
A machine-readable JSON response with:
Triage outcome (severity, type, confidence).
Counts of IOCs found.
Number of threat-intel queries and whether the email was sent.
Full investigation report content for automation or ticketing.
Note: reports are AI-generated — human review is recommended before taking actions.
SOC analysts & incident responders speed up triage and gather enrichment before manual investigation.
On-call engineers receive a single, actionable email that highlights what to check or block first.
Threat intel teams use the IOC table and enrichment as a starting point for deeper hunts.
Security managers get consistent, repeatable incident summaries for escalation and post-incident reviews.
Automation engineers integrate the JSON output into ticketing, SIEM playbooks, or orchestration workflows to accelerate response.
