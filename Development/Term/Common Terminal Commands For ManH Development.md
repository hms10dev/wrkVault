## When you want to build your component
```shell
./gradlew clean build spotlessApply
```

## Git Stash

```bash
#stash current changes:
git stash push -m '<MESSAGE>'

#create branch or switch to exisiting branch with below formatting:
#git branch <BRANCH NAME>
git branch pullrequest/AI-1459-location-labels

#Apply stashed changes to current branch
git stash apply

#add changes 
git add .
```

## Git Branch Creation Format

```bash
#git branch 'pullrequest/<Jira Story Tag>-<Message>'
git checkout master (Switch to branch)

#('-b' creates new branch)
git checkout -b pullrequest/AI-1459-location-labelsLocation-

# -d (deletes branch)
git branch -d pullrequest/AI-1459-location-labels
```

## Git Commit Format

```bash

#git commit -m '<Jira Story Tag>: <MESSAGE>'

git commit -m 'AI-1459: add location entity fields'
```

## Git Push Format

```bash

#git push -f origin <BRANCH NAME>

git push -f origin pullrequest/AI-1459-location-labels
```




## Interactive rebase to squash commit history:

```bash
# commit the new changes
git commit -a -m "Adding test changes"
# pull latest from master 
git checkout master 
git fetch
git rebase
# rebase master onto branch interactively 
git checkout pullrequest/AAL-15126-forecast-update-batch-v2
git rebase -i master
# check sublime text window for a list of commits
# to squash commits replace the 'pick' with 's' on any commits to squash
# hit save and quit sublime text
# another window will pop up to do any final updates on the commit message
# hit save and quit and rebase is complete
git push -f origin pullrequest/AAL-15126-forecast-update-batch-v2

```

# When you create a new controller and need to generate a new resource

```bash
export BUILD\_NUMBER='DATE' && ./gradlew clean build -x test && unset BUILD\_NUMBER
```
or
```bash
./gradlew buildDocker -x test -x updGradleProperties -PprodMode=true --refresh-dependencies
```
or
https://manhattanassociates.atlassian.net/wiki/spaces/OM/pages/3934061569/Generate+Resource+CI+Build+Failure
* After this , the build will fail and the terminal will tell you where to retrieve the missing resource file.

## When You want to rebase and update your local branch with newest updated master build:

```shell
git fetch                                 
git rebase origin/master 
git push --force 
```


## DB Access !

```shell
docker ps | grep my sql
```

you should see a container ID . now its time to login

```shell
docker exec -it f2b6d5df82b2 bash
```

If you want to remove the SQL container (Corrupted, health is down, etc.)
```shell
docker rm -f e9a84131d51b                                             
```