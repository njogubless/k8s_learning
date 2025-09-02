When the scheduled time for a CronJob arrives (e.g. every hour):

- A CronJob in Kubernetes is an API object that lets you run Jobs on a repeating schedule, similar to how Linux cron works.
- Job vs CronJob:
   - A Job runs a task once, until completion.

   - A CronJob creates a new Job on a defined schedule (like every hour, every day at midnight, etc.).

Use cases:
- Database backups
- Sending email reports
- Cleaning up temporary files
- Running batch data processing


1. CronJob Controller wakes up
   - The CronJob controller inside the Kubernetes control plane notices that the schedule (spec.schedule) is due.

2. A Job is created
  - The CronJob controller creates a Job object.
  - This Job is responsible for managing the execution of the task for that specific run.

3. Pods are created by the Job
  - The Job then creates one or more Pods (depending on spec.parallelism / completions) to actually execute the workload.

Each Pod runs the container specified in the CronJob template.

4. Pods run to completion
  - Unlike Deployments (which keep Pods running), Job Pods run until they succeed (or fail, if retries are exhausted).

5. Job status is recorded
  - Once the Job finishes, the CronJob updates its history/status (you can configure how many successful/failed Jobs are kept with successfulJobsHistoryLimit and failedJobsHistoryLimit).