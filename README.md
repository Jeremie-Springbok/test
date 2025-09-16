# n8n-framework-core

---

## Deploy project

1. Local - Copy Framework in a new repository: `GIT_SSH_COMMAND="ssh -i ~/.ssh/weareronin.pem" git clone git@github.com:RoninAgency/n8n-framework-core.git $PROJECT_NAME`
2. Local - Adapt project name at different locations in the code
3. Fly - Authentification: `fly auth login`
4. Fly - Launch: `fly launch --no-deploy`
5. Fly - Secrets: `fly secrets set N8N_ENCRYPTION_KEY=$`
6. Fly - Deploy: `fly deploy`

## Sync DB/Workflows with local

1. Fly - Authentification: `fly auth login`
2. Fly - SSH remote: `fly ssh console`
3. Remote - Export workflows: `su -c "n8n export:workflow --backup --output=/home/node/.n8n/workflows" node`
4. Local - Proxy Fly: `flyctl proxy 10022:22`
5. Local - Get SSH agent: `flyctl ssh issue --agent`
6. Local - Purge known host: `ssh-keygen -R '[localhost]:10022'`
7. Local - Sync script: `sh ./sync-local.sh`
8. Local - Kill proxy 
9. Local - Stop SSH agent: `fly agent stop && fly wg remove`

## Sync DB/Workflows with prod

1. Fly - Authentification: `fly auth login`
2. Local - Proxy Fly: `flyctl proxy 10022:22`
3. Local - Get SSH agent: `flyctl ssh issue --agent`
4. Local - Purge known host: `ssh-keygen -R '[localhost]:10022'`
5. Local - Sync script: `sh ./sync-prod.sh`
6. Local - Kill proxy 
7. Local - Stop SSH agent: `fly agent stop && fly wg remove`
8. Fly - Restart: `fly apps restart $PROJECT_NAME`

## Extend volume

1. Fly - Authentification: `fly auth login`
2. Fly - Identify volume: `fly volumes list`
3. Fly - Extend volume: `fly volumes extend $VOLUME_ID --size $SIZE`

## Delete App

1. Fly - Authentification: `fly auth login`
2. Fly - Deletion: `fly apps destroy $PROJECT_NAME`
