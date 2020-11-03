# Fork and clone the application config repo

In this course we will use a different repo to store the configuration needed to run your application on Kubernetes. Its name is  **java-hello-world-config** and is hosted here on GitHub as well.

In order to proceed, fork it to your GitHub account and clone it on your PC.

## Prerequisites

- A GitHub account

## Fork the repo

Open your browser and go to: https://github.com/sunnyvale-academy/java-hello-world-config

The java-hello-world-config repo home page opens.

Click on **Fork** button at the top-right of the screen. If not already, GitHub asks you to authenticate:

When you enter as logged-in user, re-click on **Fork** button at the top-right of the screen. Forking a repository allows you create a copy of the original repo on your GitHub account so as to freely experiment with changes without affecting the original project.

## Clone the forked repo

When forked the original repo, clone it on your PC.

In the following command, please make sure to change placeolders accordingly:

- \<YOUR PREFERRED FOLDER\> with the folder you want to clone this repo into
- \<YOUR GITHUB ACCOUNT\>  with your actual GitHub account (i.e. mine is denismaggior8)

```
$ cd <YOUR PREFERRED FOLDER>
$ git clone https://github.com/<YOUR GITHUB ACCOUNT>/java-hello-world-config
```

Please note that neither your forked repo, nor your local clone, will receive new commits from the original repo automatically; you need to pull updates manually, please refer to appendix [A - Sync copy of forked repo](../../appendices/A-Sync_copy_of_forked_repo/README.md)

If you need some Git help, download [**The Git cheat-sheet**](https://www.atlassian.com/dam/jcr:8132028b-024f-4b6b-953e-e68fcce0c5fa/atlassian-git-cheatsheet.pdf)
