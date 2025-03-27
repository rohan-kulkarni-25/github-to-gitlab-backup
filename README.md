# GitHub to GitLab Backup

This repo contains a GitHub Action that automatically backs up selected repositories from a GitHub organization to a GitLab group.

## How It Works

- Reads a list of selected GitHub repos from `repos.json`
- Clones each repo using `--mirror`
- Pushes it to a matching GitLab repo
- Runs daily using GitHub Actions

## Setup

1. Create two secrets in your GitHub repo:
   - GH_TOKEN: GitHub personal access token (with repo, read:org)
   - GITLAB_TOKEN: GitLab personal access token (with api, write_repository)

2. Update `repos.json` in the root of this repo with the names of the repos you want to back up.

Example `repos.json`:
{
  "repos": ["repo1", "repo2"]
}

3. Edit `.github/workflows/backup-to-gitlab.yml`:
   - Set your GitHub org name in GITHUB_ORG
   - Set your GitLab group name in GITLAB_GROUP

4. Push changes. The backup will run daily or can be triggered manually from the Actions tab.

## Notes

- GitLab repos must exist before pushing
- This uses `git clone --mirror` and `git push --mirror`
- You can extend this to create GitLab repos automatically if needed

## License

MIT
