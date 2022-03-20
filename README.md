# HelmExercise_GitHub

Set up a Helm v3 chart repository in Github

- Create a GitHub repo and name it `mygithubrepo`.

- Produce GitHub Apps Personal access tokens. Go to <your avatar> --> Settings --> Developer settings and click Personal access tokens. Make sure to copy your personal access token now. You won’t be able to see it again!

- Create a GitHub repository locally and push it.

```bash
mkdir mygithubrepo
cd mygithubrepo
echo "# mygithubrepo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/<your github name>/mygithubrepo.git
git push -u origin main
```

- Create a new chart with following command.

```bash
cd ..
helm create demogitrepo
```

- Package the repo under the `mygithubrepo` folder.

```bash
cd mygithubrepo
helm package ../demogitrepo
```

- Generate an index file in the current directory.

```bash
helm repo index .
```

- Commit and push the repo.

```bash
git add .
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
git commit -m "demogitrepo chart is added"
git push
```

- Add this repo to your repos. Go to <your repo> --> README.md and click Raw. Copy to address without README.md like below. This will be repo url.

```
https://raw.githubusercontent.com/<github-user-name>/mygithubrepo/main
```

- List the repos and add mygithubrepo.

```bash
helm repo list
helm repo add --username <github-user-name> --password <personel-access-token> my-github-repo 'https://raw.githubusercontent.com/<github-user-name>/mygithubrepo/main'
helm repo list
```

- Let's search the repo.

```bash
helm search repo my-github-repo
```

- Add new charts the repo.

```bash
cd ..
helm create second-chart
cd mygithubrepo
helm package ../second-chart
helm repo index .
git add .
git commit -m "second chart is added"
git push
```

- Update and search the repo.

```bash
helm repo update
helm search repo my-github-repo
```

- Create a release from my-github-repo

```bash
helm install github-repo-release my-github-repo/second-chart
```

- Check the objects.

```bash
kubectl get deployment
kubectl get svc
```

- Uninstall the release.

```bash
helm uninstall github-repo-release
```

