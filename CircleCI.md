### CircleCI

#### Job

- Skip build by using `[skip ci]` tag anywhere in a commit’s title or description.
- You can turn on the `Only build pull requests` feature if you don't want to build every commit.

#### Workflow

- A workflow is comprised of one or more jobs. Jobs can be run in series or parallel.
- You can enable or disable jobs per branch using branching filtering
- You can set up a scheduled workflow by using `cron` syntax
- You can also add an approval step in the workflow using `type: approval`

Here is an example of a workflow:

- `build-frontend` and `build-backend` jobs are run in parallel
- `test-frontend` job is dependent on the complete of `build-frontend` job
- `test-backend` job is dependent on the complete of `build-backend` job
- `test-integration` job is dependent on the complete of both `test-frontend` and `test-backend`
- `deploy` job is dependent on `test-frontend`, `test-backend` and `test-integration`

```
build-frontend  -> test-frontend      -> deploy
build-backend   -> test-backend       ->
                -> test-integration   ->
```

#### Workspace

- Workspace allows you to store files to be used in later jobs
- Workspace is isolated to each workflow
