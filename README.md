# Get started with the Kiro power

The Aiden for InfraOps power lets you build and deploy cloud infrastructure by chatting with the agent in [Kiro](https://kiro.dev). You describe what you need. Kiro creates the appStack in StackGen, shows you the plan, and deploys it after you approve.

This guide takes you from install to your first deploy. The same steps are on [docs.stackgen.com/infraops/kiro](https://docs.stackgen.com/infraops/kiro).

Power id: `stackgen`

## Before you start

You need:

- **Kiro**, installed and signed in.
- **A StackGen account.** You should be able to sign in at your StackGen URL (`https://cloud.stackgen.com`).
- **A StackGen role that can publish modules.** The power creates modules for your app. The **DevOps** or **Admin** role can do this. If you are not sure, ask your StackGen admin.
- **A cloud account to deploy to.** For AWS, this machine needs AWS credentials (for example, from `aws sso login`).
- **A GitHub personal access token**, only if you deploy through the StackGen SaaS runner. The runner uses it to pull your modules. You can skip this if you deploy with the local CLI. See [Step 3](#step-3-deploy-your-first-app).

You do not need to install the StackGen CLI or the AWS CLI yourself. Kiro installs or updates them the first time you use the power.

On Windows, run Kiro with WSL or Git Bash available. Some steps run bash scripts.

## Step 1: Install the power

1. In Kiro, open the **Powers** panel (the Ghosty icon with a lightning bolt).
2. Search for **StackGen**. The power is named **Aiden for InfraOps**. Some listings still show the older name, **StackGen Infrastructure as Code**. Both are the same power.
3. Select the power, then select **Install**.

You can also install from the [Kiro powers page](https://kiro.dev/powers/). Find the StackGen power and select **Add to Kiro**. Kiro opens and finishes the install.

## Step 2: Sign in to StackGen

1. On the power's detail page, select **Try power**. You can also open a new chat and type `Set up StackGen`.
2. Kiro checks for the StackGen CLI and installs or updates it.
3. A StackGen sign-in page opens in your browser. Sign in and approve the request.
4. Kiro lists your StackGen projects. Tell it which project to use.

You are connected when Kiro shows your project list.

Kiro may ask you to approve each command it runs. That is expected. If there are too many prompts, switch the chat to **Autopilot** mode.

## Step 3: Deploy your first app

Open the project you want to deploy and ask Kiro something like:

```text
Deploy this app to AWS with StackGen.
```

Kiro then:

1. Creates a new appStack and adds the resources your app needs, such as a VPC, a container service, and a load balancer.
2. Checks the appStack against your StackGen policies and fixes violations before it plans.
3. Asks you once how to run the deployment:
   - **StackGen SaaS runner** (recommended). Plan and Apply run in StackGen. Kiro asks for your GitHub personal access token.
   - **Local CLI**. Plan and Apply run on your machine with your local cloud credentials. No GitHub token is needed.
4. Runs a plan and shows you a summary. Nothing changes in your cloud account yet.
5. Waits for you to confirm. After you say yes, it applies the plan, checks that the app is healthy, and shares the appStack URL.

Every new deploy creates a new appStack. Kiro does not reuse or change existing appStacks unless you ask it to.

## Optional: ServiceNow change records

After a successful deploy, Kiro can create a ServiceNow change record through Aiden. The change number (for example, `CHG0030002`) is added to the result as your audit reference.

This step needs four values: `AIDEN_TOKEN`, `AIDEN_ORG_ID`, `AIDEN_BASE_URL`, and `AIDEN_WORKFLOW`. To check whether they are set, ask Kiro:

```text
Is the change record set up?
```

If any value is missing, the deploy still finishes. Kiro tells you that no change record was created.

## Troubleshooting

**I can't find the power.** Search for `StackGen` in the Powers panel. The listing may still use the older name, StackGen Infrastructure as Code.

**Sign-in keeps failing.** After two tries, Kiro asks you to sign in from a terminal. Run `stackgen login --url=https://cloud.stackgen.com` with your own StackGen URL, then tell Kiro to continue.

**The power worked before but now fails to connect.** The token Kiro creates lasts about two days. Type `Set up StackGen` again. Kiro signs you in and creates a new token.

**Kiro says "Permission needed" when it creates modules.** Your StackGen role can't publish modules. Ask your StackGen admin to give you the **DevOps** or **Admin** role under **Account Settings > Members**, then tell Kiro to continue.

**My company uses a different StackGen URL.** Open `~/.kiro/settings/mcp.json`. Find the StackGen server under the Powers section and change `STACKGEN_URL` to your URL, with no trailing slash. Then type `Set up StackGen` again.

**On Windows, the StackGen tools never load.** In the same file, change the StackGen server's `command` to `cmd` and its `args` to `["/c", "stackgen", "mcp"]`. Then restart Kiro.

## Related

- [Get started with the Kiro power](https://docs.stackgen.com/infraops/kiro)
- [StackGen MCP](https://docs.stackgen.com/infraops/stackgen-mcp): connect StackGen to Cursor, VS Code, or Claude without the Kiro power.
- [Create a personal access token](https://docs.stackgen.com/infraops/setup/pat): make a StackGen token by hand.
- [Configure MCP](https://docs.stackgen.com/platform/profile/configure-mcp): connect Kiro to Aiden 2.0 workspaces. That is a different server from this power.
- [Install powers](https://kiro.dev/docs/powers/installation/): Kiro's own guide to installing and updating powers.
