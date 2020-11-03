#  Configure ArgoCD to send synchronization feedback using Slack

This lab is optional, do it ONLY if you have a Slack account and you are a Workspace administrator.

## Prerequisites 

- Having completed the lab [10 - Create the first ArgoCD application](labs/10-Create_the_first_ArgoCD_application/README.md)
- Having a Slack account that is the Workspace administrator

## Install ArgoCD Notification

```console
$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj-labs/argocd-notifications/stable/manifests/install.yaml
```

## Create a Slack custom app

Create Slack Application using https://api.slack.com/apps?new_app=1 

Once application is created navigate to Enter OAuth & Permissions.

Click Permissions under Add features and functionality section and add chat:write:bot scope. To use the optional username and icon overrides in the Slack notification service also add the chat:write.customize scope. 

Scroll back to the top, click 'Install App to Workspace' button and confirm the installation.

Once installation is completed copy the OAuth token.

## Configure ArgoCD Notification

Use the OAuth token to configure the slack integration in the **argocd-notifications-secret** secret.

Before running the following command, make sure to use your Slack tocken instead of the place holder \<YOUR SLACK TOKEN\>.


```console
$ kubectl apply -n argocd -f - << EOF
apiVersion: v1
kind: Secret
metadata:
  name: argocd-notifications-secret
stringData:
  notifiers.yaml: |
    slack:
      token: <YOUR SLACK TOKEN>
type: Opaque
EOF
```

Enable built-in trigger in the argocd-notifications-cm config map:

```console
$ kubectl apply -n argocd -f - << EOF
apiVersion: v1
kind: ConfigMap
metadata:
  name: argocd-notifications-cm
data:
  config.yaml: |
    triggers:
      - name: on-sync-succeeded
        enabled: true
EOF
```

Subscribe to notifications by adding the recipients.argocd-notifications.argoproj.io annotation to the Argo CD application or project (make sure you put the channel name instead of \<my-channel\> and the application name instead of \<my-app\>):

```console
$ kubectl patch app <my-app> -n argocd -p '{"metadata": {"annotations": {"recipients.argocd-notifications.argoproj.io":"slack:<my-channel>"}}}' --type merge
```

In my case, I created a Slack channel named **#java-hello-world** (as the application name), so as my command is:

```console
$ kubectl patch app java-hello-world-development -n argocd -p '{"metadata": {"annotations": {"recipients.argocd-notifications.argoproj.io":"slack:java-hello-world"}}}' --type merge
application.argoproj.io/java-hello-world-development patched
```

Before testing the solution, invite the Slack bot you created in the channel **java-hello-world** by mentioning him in the channel.

## Test the notification

To test the notification, just manually force a Sync operation on the application you created in the previous lab. 

```console
$ argocd app sync java-hello-world-development 
...
Message:            successfully synced (all tasks run)
...
```

If the solution worked, you should see a message like this on you Slack channel

![](img/1.png)


