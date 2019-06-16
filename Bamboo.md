### Bamboo

[Bamboo CI Server Overview](https://confluence.atlassian.com/bamboo/files/289277285/289342279/2/1426549208892/CI+overview.png)

[Bamboo Structure](https://confluence.atlassian.com/bamboo/files/289277285/319619101/1/1359074967455/BambooPlanAnatomy.png)

In Bamboo, you need to first create a `plan`. Different plans can run in parallel or in sequence. Each plan is associated with a `project`, a project is just a grouping of plans in Bamboo.

Plan needs to be triggered to run. You can trigger a plan by the following ways:

- code change
- daily
- scheduled (cron job)
- manually
- completion of another plan

Plan needs to get code to run from a repository. When creating a plan, you can select which repository and branch the plan is associated with.

A plan is made of at least one `stage` and can have several stages. Stages are executed sequentially.

A stage is made of at least one `job` and can have several jobs, a job is a unit of execution. If there are multiple jobs in a stage, those jobs will be executed in parallel. Every job can protentially produce an `artifact` once it's complete successfully. The aggregation of all the artifacts produced by jobs is actually the artifact of a stage, which can be passed to the next stage.

A job is made of at least one `task` and can have several tasks. Tasks are executed sequentially within a job.
