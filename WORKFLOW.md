---
tracker:
  kind: github
  api_key: $GITHUB_TOKEN
  owner: rpgeddam
  repo: symtest
  active_states:
    - Todo
  active_labels:
    - todo
    
workspace:
  root: /tmp/symphony_workspaces
  
hooks:
  after_create: |
    git clone https://x-access-token:${GITHUB_TOKEN}@github.com/your-user/your-repo.git .
  before_run: |
    git fetch origin
    git checkout -b feature/{{ issue.identifier }}
    git reset --hard origin/main
    
codex:
  command: codex app-server
---

You are working on {{ issue.identifier }}: {{ issue.title }}.

{{ issue.description }}

When done:
1. Commit your changes
2. Push the branch: git push -u origin HEAD
3. Create a PR using: gh pr create --title "{{ issue.title }}" --body "Closes {{ issue.identifier }}"
4. Move the issue to Done
