# Aiden for InfraOps

Kiro power for designing and deploying cloud infrastructure with StackGen. You describe the app in chat. Kiro creates an appStack, shows the plan, and deploys after you approve.

Power id: `stackgen`

## Install

1. In Kiro, open the Powers panel.
2. Search for **StackGen**. The power is listed as **Aiden for InfraOps**. Older listings may still say **StackGen Infrastructure as Code**.
3. Select **Install**.

You can also install it from [kiro.dev/powers](https://kiro.dev/powers) with **Add to Kiro**.

## Sign in

1. Open the power and select **Try power**, or start a chat and type `Set up StackGen`.
2. Approve the StackGen sign-in page in your browser.
3. When Kiro lists your projects, tell it which project to use.

You need a StackGen account and the **DevOps** or **Admin** role so the power can publish modules.

## First deploy

In the project you want to deploy, ask:

```text
Deploy this app to AWS with StackGen.
```

Kiro creates a new appStack, runs a plan, and waits for you to approve before it applies anything.

## Docs

Install, sign-in, and troubleshooting: [Get started with the Kiro power](https://docs.stackgen.com/infraops/kiro).
