# smda-trunkbased
trunk based repo sample
## https://www.nebulaworks.com/insights/posts/trunk-based-development-for-beginners/
1. git clone git@github.com:<repopath>.git
2. Create a new branch off master. Make this branch’s name related to the work being done. In this case, the feature branch is tied to an issue that I have spun out in a ticketing platform (jira, gitlab board, etc).

### git checkout -b mr/issue-1             # mr are my initials
## [Key Concept] We are creating a new branch to ensure that master is always in a deployable state. We do not want to introduce changes that could potentially break code in master. Whenever we want to add a new feature to our codebase a new branch will be created to develop and test said feature.
## On our new branch let’s create a python script that lets us know why TBD is awesome! We will be adding and commiting the script to our repository.
### cat << EOF > tbd-script.py
### print("Trunk-Based Development is awesome!")
### EOF
## git add tbd-script.py
## git commit -m "Added tbd python script"
## [Key Concept] Before we are able to merge our new feature into masterwe will run tests to verify that our feature works. Running python3 tbd-script.py will output Trunk-Based Development is awesome! to the terminal. For this simple feature, a test like this is satisfactory. In reality, your code should be subject to meaningful tests.

## After having your PR reviewed, if further changes are needed, repeat steps 2 and 3.
## If everything looks good a team member will merge your PR!

## [Key Concept] Your PR MUST be approved and merged by someone who did not contribute any commits to the new branch. The more eyes we have on our code, the better the quality.

## Good job so far! We have successfully added a new feature into our master branch. Now everyone will know how great TBD is! Let’s start working on our second feature.
Creating Our Second Feature
Let’s pull and rebase remote master onto our local master branch.

git pull --rebase origin master
[Key Concept] Since our PR was approved and merged in Github, we need to make sure that our local master branch is up to date with our remote master. We are treating both masters as one and the same!

Note: We’re using the --rebase flag to make sure that our local master’s history aligns with the remote. It also prevents any ugly merge bubbles!
Now that our local master branch is up-to-date let’s get started on issue-2. We’ll repeat step 1.

Let’s add some new functionality!
cat << EOF > tbd-script.py
print("Trunk-Based Development is awesome!")
print("It allows for fast iteration!")      # new line added
EOF
git add tbd-script.py
git commit -m "Adding new print statement to tbd script"
Let’s push our code up to Github.

git push origin mr/issue-2
We should perform any tests that we need to validate the new functionality. Running python3 tbd-script.py will show us output that we can validate.
Rebasing:
Now that we’ve verified our feature works as expected, let’s open up a PR for the mr/issue-2 branch.

[Key Concept] Uh oh. It looks like our PR is showing merge conflicts with master. Another developer on our team created a branch for feature 3 called al/issue-3. It looks like al/issue-3 was already merged into master. During development, it is common to have PRs being merged into master after our issue branch was originally branched from master. We need to get these new commits onto our mr/issue-2 branch. This process is known as rebasing.
First, let’s update our local master branch

git checkout master

git pull --rebase origin master

Let’s grab the latest commits from our local master branch, and get them into our branch.

git checkout mr/issue-2

git rebase master
[Key Concept] Frequent rebasing is encouraged in the TBD workflow. As all developers are iterating on master, it will be updated constantly. git rebase allows us to temporarily remove any commits made on our branch, apply the missing commits from master onto our branch and then reapply our commits on top of them. This ensures that we’re keeping master’s commit history consistent across all branches.

Note: During the rebase you might have to deal with conflicts, this is expected and unavoidable if there are changes

Now that our branch is up-to-date, we should re-test our branch, make any necessary changes and push to our remote.

git push origin mr/issue-2 -f
Since we have added new commits to our branch’s git history, we need to pass in the -f flag. This will allow git to overwrite the history of the remote branch. If we don’t do this Git will error out when it sees that the local and remote mr/issue-2 branch’s history differ.

Note: Our existing PR will be updated with any changes made to our branch.

