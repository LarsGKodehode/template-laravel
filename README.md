# Laravel Template Project

## Content

- [Setup](#setup)
- [Notes](#notes)
  - [Terminals](#terminals)
  - [Other](#other)
  - [Deployments](#deployments)
  - [Sidenotes](#sidenotes)

<br><hr>

## Setup

1. Install Docker Desktop
  - [Windows](https://docs.docker.com/desktop/install/windows-install/)
  - [iOS](https://docs.docker.com/desktop/install/mac-install/)
  - [Linux Distro](https://docs.docker.com/desktop/install/linux-install/)

2. Install the VS Code extension for working inside [devcontainers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

3. Clone this repository
```sh
git clone $REPO_URL
```

4. Install PHP dependencies
```sh
docker run --rm \
    --pull=always \
    -v "$(pwd)":/opt \
    -w /opt \
    laravelsail/php82-composer:latest \
    bash -c "composer install"
```
This downloads a temporary container with the software to install the required dependencies to get up and running

5. Copy over the .env file, [configure it](https://laravel.com/docs/10.x/configuration#introduction)
```sh
cp .env.example .env
```

6. Start the development server
```sh
./vendor/bin/sail up
```

7. [FIX THIS] Open Docker Desktop and open a terminal into the main container (not sql and not redis) and run
```sh
chown -R 1000:1000 /var/www/html
```

8. Open VS Code inside the repository **AND THEN** run (Ctrl + Shift + P) ```Dev Container: Open folder in Container```

9. Generate a new APP_KEY
```sh
php artisan key:generate
```

10. You should now be able to open a browser at [http://localhost](http://localhost) and see something

11. Install Node dependencies
```sh
npm install
```

12. Create tabels for your local database
```sh
php artisan migrate
```

13. Start the deveolopment server
```sh
npm run dev
```

14. Start editing files

<br><hr>

## **Notes**

## Terminals

You will be working with 2 (two) terminals for this project

1. Your OS terminal of choice. You will use this for project commands ex:
  - ```git``` <br>
    Simplify tracking changes to your project
  - ```docker```
    It's possible to run containers inside containers, but thats an advanced topic
  - ```./vendor/bin/sail```
    Similar as above, due to sail just being a wrapper around docker

2. Terminal inside VS Code. This will be used for running commands inside the project
  - ```composer <command>``` installing packages
  - ```php <command>``` installing packages and interacting withg the artisan CLI
  - ```npm <command>``` administrating package.json++

## Other

The **.env** file containes secrets that should not be shared with 3rd parties, and hence is excluded from the Version Control System. Be mindeful of not losing the content from it, or keep some instructions around for regenerating those.

## Deployments

I am a little bit uncertain about what the best deployment method for PHP applications are.
Two alternatives that [Laravel reccomends](https://laravel.com/docs/10.x/deployment)

- [Forge](https://forge.laravel.com/#pricing)
- [Vapor](https://vapor.laravel.com/)

## Sidenotes

- After installing and setting up [Breeze](https://laravel.com/docs/10.x/starter-kits#laravel-breeze) you might have to run ```php artisan view:clear``` to clear out any reminders from the default setup process. [StackOverflow](https://stackoverflow.com/a/72821399)

- When running Vite in development mode it places a file [/public/hot](./public/hot), this should be removed automatically when stopping the server. But there have been some [reported issues](https://laracasts.com/discuss/channels/vite/laravel-vite-err-address-invalid?page=1&replyId=872112) that this is not always the case, which breaks production. If you have any problems check if that file exists and remove it.