# Github CLI on Ubuntu

> 17/09/2023 - Erwin van Hoof

## Why?
Working from the shell is way easier the clicking around on github. 

## How?

### Installation 

```
type -p curl >/dev/null || (sudo apt update && sudo apt install curl -y)
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
&& sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
&& sudo apt update \
&& sudo apt install gh -y
```
> **Note**
> Github was recently forced to change our GPG signing key. If you've previously downloaded the `githubcli-archive-keyring.gpg` file, you should re-download it again per above instructions. If you are using a keyserver to download the key, the ID of the new key is `23F3D4EA75716059`.

## Setup

Authenticate with GitHub by running this command from your terminal.
```
gh auth login
```
Follow the on-screen prompts.

## Quickstart 

### Viewing your status
Enter ```gh status``` to see details of your current work on GitHub across all the repositories you're subscribed to.

### Viewing a repository
Enter ```gh repo view OWNER/REPO``` to see the repository description and README.md for the repository. Enter ```gh repo view OWNER/REPO --web``` to view the repository in your default browser.

If you run the repo subcommand from within the directory of a local Git repository that has a remote on GitHub you can omit OWNER/REPO.

### Cloning a repository
Enter ```gh repo clone OWNER/REPO```. For example,```gh repo clone octo-org/octo-repo``` clones the octo-org/octo-repo repository to the directory from which you ran this command on your local computer.

### Creating a repository
Enter ```gh repo create``` and follow the on-screen instructions. You can create a new, empty repository on GitHub and then, optionally, clone it locally. Alternatively, you can push an existing local repository to GitHub, and optionally set it as the remote for your local repository. For information on setting a local directory as a Git repository, see "Adding locally hosted code to GitHub."

To add a local repository to the newly created repo: 
See: https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github#adding-a-local-repository-to-github-using-git


### Working with issues
Enter gh issue list --repo OWNER/REPO to list the most recently created issues that are currently open for the specified repository. If you run the issue subcommand from within the directory of a local Git repository that has a remote on GitHub you can omit --repo OWNER/REPO. For example, enter gh issue list --assignee "@me" to list issues assigned to you in this repository, or gh issue list --author monalisa to list issues created by the user "monalisa."

You can also create a new issue, see "Creating an issue," or search for an issue, see "Filtering and searching issues and pull requests."

### Working with pull requests
Enter ```gh pr list --repo OWNER/REPO``` to list the most recently created pull requests that are currently open for the specified repository. If you run the pr subcommand from within the directory of a local Git repository that has a remote on GitHub you can omit --repo OWNER/REPO. For example, enter gh pr list --author "@me" to list open pull requests that you created in this repository.

Enter ```gh pr list --label LABEL-NAME``` to list open pull requests with a specific label. Enter ```gh search prs --review-requested=@me --state=open``` to list pull requests that you've been asked to review.

To create a pull request, enter ```gh pr create``` and follow the on-screen instructions. For more information, see "Creating a pull request."

### Working with codespaces
To create a new codespace, enter ```gh codespace``` create and follow the on-screen instructions.

To display your existing codespaces, enter ```gh codespace list```. To open a codespace in the web version of VS Code enter gh codespace code -w and choose a codespace .

In all of these commands you can substitute cs for codespace.
