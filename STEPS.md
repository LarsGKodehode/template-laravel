# Steps for setting this up

1. Install Docker Desktop
  - [Windows](https://docs.docker.com/desktop/install/windows-install/)
  - [iOS](https://docs.docker.com/desktop/install/mac-install/)
  - [Linux Distro](https://docs.docker.com/desktop/install/linux-install/)
2. Install the VS Code extension for working inside [devcontainers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
3. Clone this repository
```sh
git clone $REPO_URL
```
4. Open VS Code inside the repository **AND THEN** run (Ctrl + Shift + P) ```Dev Container: Open folder in Container```
5. Start the development server from the original terminal
```sh
./vendor/bin/sail up
```

## Notes

You will be working with 2 (two) terminals for this project

1. Your OS terminal of choice. You will use this for project commands ex:
  - ```git``` <br>
    Simplify tracking changes to your project
  - ```docker```
    It's possible to run containers inside containers, but thats an advanced topic
  - ```./vendor/bin/sail```
    Similar as above, due to sail just being a wrapper around docker
2. VS Code terminal. This will be used for running commands inside the project
  - ```composer <command>``` installing packages
  - ```php <command>``` installing packages and interacting withg the artisan CLI


## Sidenotes

Commments for those who want to set this up themself

- After installing and setting up breeze you might have to run ```php artisan view:clear``` to clear out any reminders from the default setup process. [StackOverflow](https://stackoverflow.com/a/72821399)