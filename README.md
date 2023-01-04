# GitHub Workflow for SSG on Forest
Proof of concept for triggering new builds on Forest.
The idea is:
- DatoCMS (or anything really) calls GitHub webhook
- Webhook triggers workflow
- Workflow commits to branch X
