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