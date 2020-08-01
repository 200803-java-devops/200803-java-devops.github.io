# Git
Git is a source code management system that can save snapshots of your project on one or more branching paths.

## Glossary
- **Repository**: Files, folders, objects, and branches representing a project, managed within a `.git` folder
- **Working Directory**: Currently active project files and folders.
- **Staging Area**: Area between Working Directory and Repository where project changes are added before the next commit.
- **Commit**: Snapshot of staged changes from a working directory.
- **Branch**: Named pointer to a commit in git history.
- **Head**: Special pointer to the current branch.
- **Remote**: Link to synchronized external repository, usually on a service like GitHub.
- **.gitignore**: Text file listing what to ignore when moving working directory files into staging.

## Flow
After initializing a new git repository in a working directory (`git init`) its files and folders must be added to its staging area (`git add [files]`) before they can be saved (`git commit`). 

New changes in the working directory must be staged and then committed again. New branches can be created or users can switch to an existing branch (`git checkout`) to explore divergant changes, then eventually combined (`git merge`). 

If a local repository is linked to a remote repository, changes made locally can be copied to the remote location (`git push`), and changes in the remote repository can be copied down to the local version (`git pull`).

## Example commands
```bash
# Initialize a git project
git init

# Add specific files and folders
git add <FILE NAME>

# Commit staged changes with a message
git commit -m "<YOUR MESSAGE>"

# List all branches
git branch

# Checkout an existing branch
git checkout <BRANCH NAME>

# Reset code back to last commit
git reset --hard

# Checkout a new branch based on current branch
git checkout -b <BRANCH NAME>

# Stash outstanding changes (to cleanly switch branches)
git stash

# Retrieve previously stashed changes
git stash pop
```

## Remote Repositories
Cloud services like GitHub, GitLab, and BitBucket host git servers which can be synchronized with local repositories. When an existing project on these services is cloned, its `.git` directory will include a remote link to the original project, commonly known as `origin`.

A local repository can also be synchronized in the opposite direction, copying a local project to an empty repository on a cloud server.

```bash
# Create remote link named 'origin'
git remote add origin <REMOTE URL>

# Push local master branch to origin master branch
git push -u origin master

# Copy remote git repository to local folder
git clone <REMOTE URL>
```

## Pull Requests
On remote git server services like GitHub, other users are able to "fork" a repository, which creates a copy of that project on their own account. If a user clones the repository and pushes changes, they may open a "pull request" back to the original project, requesting a review of their work and to either accept or deny merging these changes.

## Resources
### Articles
- [Understanding the GitHub flow](https://guides.github.com/introduction/flow/)

### Books
- [Pro Git](https://git-scm.com/book/en/v2)

### Documentation
- [Git Documentation](https://git-scm.com/doc)
- [Git Configuration](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)

### Tutorials
- [GitHub - Resources to learn Git](http://try.github.io/)
- [Visualizing Git](https://git-school.github.io/visualizing-git/)
- [Git](https://www.vogella.com/tutorials/Git/article.html)
[GitHub Pull Request Tutorial](https://help.github.com/en/articles/creating-a-pull-request-from-a-fork)