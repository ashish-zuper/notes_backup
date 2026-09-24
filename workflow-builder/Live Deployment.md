# Create a new branch from the last known good production state
git checkout -b deploy-hotfix <last-production-commit-or-tag>

# Cherry-pick only the hotfix commit
git cherry-pick <hotfix-commit-id>

# Create and push the tag
git tag -a v1.2.3-hotfix -m "Hotfix deployment"
git push origin deploy-hotfix
git push origin v1.2.3-hotfix


