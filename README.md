# Jellyfin Docker Compose Deployment

Personal Jellyfin media server deployment configuration using Docker Compose.

## Configuration

- **Image**: jellyfin/jellyfin:10.11
- **Ports**: 8096 (HTTP)
- **GPU**: Enabled for hardware transcoding
- **User**: 420:420

### Volumes

- `./config` - Jellyfin configuration
- `./cache` - Jellyfin cache
- `./data` - Jellyfin data
- `/allmedia/TV` - TV shows
- `/allmedia/Movies` - Movies
- `/allmedia/Strange-Things` - Strange Things content

## Branch Workflow

- **trunk**: Main development branch - push changes here for testing and development
- **prod**: Production branch - Coolify auto-deploys from this branch
- To deploy: merge or push changes from `trunk` to `prod`

## Coolify Auto-Deploy Setup

To set up auto-deploy from GitHub to Coolify:

1. **In Coolify**:
   - Navigate to your Jellyfin service
   - Change the source from "Docker Compose" to "Git Repository"
   - Set Git repository URL: `https://github.com/zachg-devops/jellyfin-compose`
   - Set branch: `prod`
   - Set build pack to "Docker Compose"
   - Enable "Automatic Deployment" toggle
   - Copy the webhook URL from Coolify

2. **In GitHub**:
   - Go to repository Settings → Webhooks
   - Add webhook with the Coolify webhook URL
   - Content type: `application/json`
   - Trigger: "Just the push event"
   - Save webhook

3. **Test**: Push a change to the repository and verify Coolify automatically redeploys

## Local Development

```bash
docker compose up -d
```

## Notes

- Config, cache, and data directories are gitignored as they contain runtime data
- Ensure the user UID:GID (420:420) has access to the media directories
- GPU passthrough requires proper NVIDIA drivers on the host
