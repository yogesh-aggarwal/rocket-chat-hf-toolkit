# 🤗 Hugging Face TeamFlow for Rocket.Chat

Transform your Rocket.Chat into a powerful ML team collaboration hub. Manage Hugging Face resources, coordinate team efforts, and streamline ML workflows - all without leaving your chat.

## 🎯 Why HF TeamFlow?

Unlike the standard Hugging Face dashboard, HF TeamFlow brings team-first features that make ML collaboration seamless:

### 1. Team-First Model Governance
```bash
/hf deploy fraud-model-v2 --approval-flow strict
```
✨ Creates structured approval workflow with:
- Model diff summaries in thread
- Required approver pings (@ml-lead, @security)
- Reaction-based approvals (👍)
- Auto-generated compliance docs
- Complete audit trail

### 2. ML Incident War Rooms
```bash
/hf incident create bert-prod --type accuracy-drop
```
✨ Instant collaboration context:
- Dedicated debug thread
- Auto-pulled logs and metrics
- Structured debug checklist
- Team pings and assignments
- Auto-generated post-mortems

### 3. Smart Cost Management
```bash
/hf budget demo-space --alert-threshold 100
```
✨ Team-based cost control:
- Real-time spending alerts
- Budget increase requests via reactions
- Auto-shutdown rules
- Cost attribution tracking
- Team expense reports

### 4. Knowledge Capture
```bash
/hf document bert-v2 --from-thread
```
✨ Turn chat into documentation:
- Convert discussions to model cards
- Auto-tag key decisions
- Link discussions to versions
- Maintain decision history
- Generate compliance docs

### 5. AI-Powered Reviews
```bash
/hf review model-card bert-v3 --ai-assist
```
✨ Automated quality checks:
- Model card completeness check
- Ethical concern flagging
- Similar model comparison
- Security vulnerability scan
- Team review workflow

## 🛠️ Command Reference

Each command is mapped to specific Hugging Face API endpoints. Here's a detailed breakdown:

### Authentication & Setup

```bash
# User Authentication
/hf login [token]              # Set your HF access token
/hf logout                     # Remove your token
/hf status                     # Check authentication status
/hf settings                   # Configure app settings

API Endpoints:
- Validate Token: GET https://huggingface.co/api/whoami
- User Info: GET https://huggingface.co/api/users/{username}
```

### Model Management

```bash
# List & Search Models
/hf models list               # List your models
/hf models search [query]     # Search models
    --author [name]          # Filter by author
    --task [type]           # Filter by task
    --framework [name]      # Filter by framework
    --sort [downloads|likes] # Sort results

API Endpoints:
- List Models: GET https://huggingface.co/api/models
- Search Models: GET https://huggingface.co/api/models?search={query}
- Model Info: GET https://huggingface.co/api/models/{model_id}

# Model Information & Updates
/hf model info [model-id]     # Get model details
/hf model card [model-id]     # View model card
    --edit                   # Edit model card
    --update [field] [value] # Update specific field

API Endpoints:
- Get Model Card: GET https://huggingface.co/api/models/{model_id}/card
- Update Model Card: POST https://huggingface.co/api/models/{model_id}/card
- Update Tags: POST https://huggingface.co/api/models/{model_id}/settings

# Model Deployment
/hf deploy [model-id]         # Deploy model
    --approval-flow [strict|standard]
    --reviewers [@user1,@user2]
    --environment [prod|staging]

API Endpoints:
- Create Deployment: POST https://huggingface.co/api/models/{model_id}/deploy
- Get Status: GET https://huggingface.co/api/models/{model_id}/deployment
```

### Space Management

```bash
# Space Operations
/hf space list                # List Spaces
/hf space status [space-id]   # Get Space status
/hf space logs [space-id]     # View logs
    --tail [number]         # Show last N lines
    --follow               # Stream logs
/hf space restart [space-id]  # Restart Space

API Endpoints:
- List Spaces: GET https://huggingface.co/api/spaces
- Space Info: GET https://huggingface.co/api/spaces/{owner}/{space_id}
- Space Logs: GET https://huggingface.co/api/spaces/{owner}/{space_id}/logs
- Hardware Info: GET https://huggingface.co/api/spaces/{owner}/{space_id}/hardware

# Space Monitoring
/hf space monitor [space-id]  # Set up monitoring
    --alerts [cpu|memory|error]
    --threshold [value]
    --notify [@user|#channel]

API Endpoints:
- Metrics: GET https://huggingface.co/api/spaces/{owner}/{space_id}/metrics
- Runtime: GET https://huggingface.co/api/spaces/{owner}/{space_id}/runtime
```

### Team Collaboration

```bash
# Incident Management
/hf incident create          # Create incident
    --type [error-type]
    --severity [1-5]
    --mention [@user1,@user2]
/hf incident update         # Update incident
    --status [status]
    --add-logs [url]

Integration Points:
- Creates structured threads in Rocket.Chat
- Links to HF model/Space status
- Integrates with webhook events

# Documentation Generation
/hf document [model-id]      # Generate documentation
    --from-thread [thread-id]
    --from-channel [duration]
    --sections [section1,section2]

API Endpoints:
- Get Model Card: GET https://huggingface.co/api/models/{model_id}/card
- Update Model Card: POST https://huggingface.co/api/models/{model_id}/card
```

### Cost & Resource Management

```bash
# Budget Control
/hf budget status            # Overall budget status
/hf budget set [space-id]    # Set budget limits
    --daily [amount]
    --alert [amount]

API Endpoints:
- Space Usage: GET https://huggingface.co/api/spaces/{owner}/{space_id}/metrics
- Billing Info: GET https://huggingface.co/api/organizations/{org}/billing

# GPU Management
/hf gpu request [type]       # Request GPU resources
    --hours [number]
    --priority [high|normal]
    --notify-when-free

API Endpoints:
- Hardware Status: GET https://huggingface.co/api/spaces/{owner}/{space_id}/hardware
- Update Hardware: POST https://huggingface.co/api/spaces/{owner}/{space_id}/hardware
```

### Webhook Integration

```bash
Available Events:
- repo-updated
- discussion-created
- pr-opened
- pr-closed
- space-status-updated

Webhook URL Format:
POST https://huggingface.co/api/repos/{owner}/{repo}/hooks

Event Payload Example:
{
  "event": "repo-updated",
  "repo": {
    "name": "model-name",
    "owner": "username",
    "sha": "commit-hash"
  }
}
```

## 🎨 Interactive Features

- **Reaction-Based Actions**
  - 👍 Approve changes
  - 🔍 Request review
  - ⚡ Escalate incident
  - 💰 Request budget increase

- **Thread Management**
  - Auto-created for incidents
  - Structured debug checklists
  - Decision tracking
  - Knowledge capture

- **Real-Time Updates**
  - Training progress
  - Space status
  - Cost alerts
  - Security notifications

## 🔧 Setup

1. Install from Rocket.Chat marketplace
2. Configure in Administration panel
3. Users authenticate: `/hf login [token]`
4. Set up team notifications: `/hf watch`

## 🔐 Security & Compliance

- Encrypted token storage
- Role-based access control
- Full audit logging
- Compliance documentation
- Security scanning

## 📋 Requirements

- Rocket.Chat 5.0+
- Hugging Face Pro account (some features)
- Webhook-capable environment

## 🤝 Contributing

See [Contributing Guide](CONTRIBUTING.md) for details.

## 📜 License

MIT License - see [LICENSE](LICENSE)

## 🆘 Support

- GitHub Issues
- #hf-teamflow-support channel
- support@example.com

---

Built with 🤗 for ML teams