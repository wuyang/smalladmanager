# Small Ad Manager
This project aims to build a fully functional system similar to Google Ad Manager, but one that can run on a laptop. As a result, scalability has been sacrificed.
It is built based on public information and assisted by AI technologies like ChatGPT.

Google Ad Manager Help Center: https://support.google.com/admanager/?hl=en#topic=7505988

Google Ad Manager Reporting SOAP API: https://developers.google.com/ad-manager/api/reporting#python

Report call flow

```mermaid
sequenceDiagram
    participant Client
    participant API Server
    participant Report Manager
    participant Report Executor
    participant Report Storage
    Note over API Server: Stateless
    Note over Report Manager: Stateful and persistent
    autonumber
    Client ->> API Server: RunReport API
    API Server ->> Report Manager:CreateReport API
    Report Manager ->> API Server: Return report id
    API Server ->> Client: Return report id
    Report Manager ->> Report Executor: ExecuteReport API
    Report Executor ->> Report Storage: Save Report
    Report Executor ->> Report Manager: NotifyReportStatus API
    Client ->> API Server: PollReportStatus API
    API Server ->> Report Manager:PollReportStatus API
    Report Manager ->> API Server: Return report download URL if ready
    API Server ->> Client: Return report download URL if ready
```

