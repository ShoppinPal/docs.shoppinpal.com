# How to Handle Support Incidents

Best practices for resolving support incidents:

1. ask the customer for the full problem statement
2. ask the customer for the time window within which they need a workaround versus a complete fix
3. determine if the problem can be reproduced on staging or production without changing the customer's data
4. always reproduce the issue if possible without changing the customer data so that you can view the problems in server logs or worker logs, live.
    * Otherwise tell the customer that it will take longer and inspect older logs ... this means gaining customer consent for a larger time window to get them any workarounds/fixes.
5. if inspecting older logs is taking too long or is impossible to find data in time for the customer's needs ... then ask customer for permission to reproduce the issue live and inform them how it will change their staging/production data and what the cleanup steps (if any) may be
6. always keep the customers appraised of the situation and if more time is required or the situation simply cannot move forward for sometime ... be honest and let them know.