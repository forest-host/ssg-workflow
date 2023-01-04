# GitHub Workflow for Static Site Generation on Forest
Proof of concept for triggering new builds on Forest.

## :earth_africa: Resource usage
Please be aware: SSG is very cool and hip but also majorly resource intensive.
HTTP caches like Varnish are very able to easily reach the same level of performance optimalisation as SSG.
Before using this workflow consider switching to Server Side Rendered. Forest
has Varnish HTTP caching build-in, no need to configure that.

## How it works
For Forest to create a new build a new commit is required.
This makes sure Forest wont use a cached build from an existing commit.
This workflow commits to a specified branch (`production`) in this example, each
time the workflow is triggered.
The workflow can be triggered manually from GitHub or by calling a webhook.

## How to use
1. Copy the workflow to your project
2. Edit the workflow accordingly, watch for:
    - What branch to use? (this is the branch you'll use to deploy to Forest)
3. Setup your trigger (read on)

**Triggering the workflow**
The workflow can be triggered manually in GitHub (github.com/repo > Actions > `Push-to-Forest` > Run workflow)
or by using a webhook.
This example uses curl to trigger the workflow on this repository:
```
curl -X POST https://api.github.com/repos/Forest-Host/ssg-workflow/dispatches \
    -H "Authorization: token {PERSONAL_DEVELOPER_TOKEN}" \
    -H "Content-Type: application/json" \
    -d '{"event_type": "webhook"}'
```
Breaking it down you'll need a [personal GitHub token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
to authenticate the request. Add this as a header: `Authorization: token {PERSONAL_DEVELOPER_TOKEN}`

The url is build up of your user/organisation and repository. Like:
`https://api.github.com/repos/{USER}/{REPOSITORY}/dispatch`

The body should include the event type name as stated in the workflow, by
default that is: `{"event_type": "webhook"}`
