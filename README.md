# Network Monitoring & Automation Pipeline (Sanitized Overview)

## Context
This repository provides a high-level, sanitized overview of an automated
network monitoring and log processing pipeline developed during an
IT Infrastructure internship.

Due to **confidentiality and security considerations**, internal source code,
configurations, and deployment details are **intentionally omitted**.

## High-Level Architecture
- Periodic network traffic capture using tcpdump
- Time-based PCAP rotation (per-minute) with timestamped directories
- Log generation and parsing using Zeek
- Centralized log ingestion and processing using Python
- File-based state management to ensure idempotent processing

## Simplified Orchestration Logic (Pseudocode)
```
LOOP every fixed interval:
    capture network traffic into a timestamped PCAP file

FOR each new PCAP batch:
    generate structured logs using Zeek
    group logs into a timestamped directory

FOR each incoming log directory on analysis server:
    IF directory is not marked as processed:
        process logs for monitoring and alerting
        mark directory as processed (.done)

IGNORE directories already marked as processed
```

## Automation Flow (Simplified)
1. Bash automation triggers tcpdump on a fixed interval
2. PCAP files are written using timestamp-based naming
3. Zeek processes each capture batch to generate structured logs
4. Log directories are transferred to a centralized analysis server
5. Python automation processes new folders and marks completion using `.done` flags

## Design Considerations
- Physically isolated test environment (dedicated router, switch, modem, personal laptop as server)
- No unsupervised interaction with production systems
- Architecture reviewed and validated by senior network engineers
- Testing activities were supervised and assisted by senior network engineers and the cybersecurity team
- Emphasis on reliability, repeatability, and operational safety
- Designed to work without databases or message queues due to scope constraints

## Skills Demonstrated
- Network automation and monitoring
- Infrastructure scripting (Bash, Python)
- Log-based alerting workflows
- File-based state management
- Enterprise IT governance awareness
