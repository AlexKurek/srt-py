## Small Radio Telescope Docs
#### Internal Port Mapping

| Purpose                   | Port  | From      | To                       |
|---------------------------|-------|-----------|--------------------------|
| Status Updates            |  5555 | Daemon    | Dashboard                |
| Command Queue             |  5556 | Dashboard | Daemon                   |
| GNU Radio XMLRPC          |  5557 | Daemon    | GNU Radio                |
| Raw I/Q Data w. Tags      |  5558 | GNU Radio | Daemon, User (Opt.)      |
| Raw I/Q Data w/o Tags     |  5559 | GNU Radio | Dashboard, User (Opt.)   |
| Raw Spec. w. Tags         |  5560 | GNU Radio | User (Opt.)              |
| Raw Spec. w/o Tags        |  5561 | GNU Radio | Dashboard, User (Opt.)   |
| Calibrated Spec. w. Tags  |  5562 | GNU Radio | Daemon, User (Opt.)      |
| Calibrated Spec. w/o Tags |  5563 | GNU Radio | Dashboard, User (Opt.)   |
| Dashboard Webpage         |  8080 | Dashboard | User                     |