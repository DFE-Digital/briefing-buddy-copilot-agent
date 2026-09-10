# briefing-buddy-copilot-agent
A Copilot Studio agent for BriefBuddy.

## Setting up the Copilot agent locally

Follow these steps to get the agent source synced to your machine using the Power Platform CLI (`pac`).

### 1. Install the Power Platform CLI

```bash
dotnet tool install --global Microsoft.PowerApps.CLI.Tool
```

> Requires the [.NET SDK](https://dotnet.microsoft.com/download) to be installed first.

Verify the install:

```bash
pac help
```

### 2. Authenticate with your Power Platform environment

```bash
pac auth create --environment <environment-url-or-id>
```

### 3. Clone the agent (first-time setup)

If you don't have a local folder for the agent yet, clone it from Copilot Studio:

```bash
pac copilot clone --bot <agent-id> --environment <environment-id>
```

- **`<environment-id>`**: In the [Power Platform admin center](https://admin.powerplatform.microsoft.com/), go to **Environments** > select your environment, and copy the **Environment ID** from the environment details pane. You can also find it in the URL when working in Copilot Studio or Power Apps for that environment.
- **`<agent-id>`**: In [Copilot Studio](https://copilotstudio.microsoft.com/), open the agent, go to **Settings** > **Advanced** > **Metadata**, and copy the **Schema name**. Alternatively, it appears in the browser URL when editing the agent, e.g. `copilotstudio.microsoft.com/environments/<environment-id>/bots/<agent-id>/...`.

This creates a new local folder (named after the agent) containing its topics, workflows, knowledge sources, and settings.

### 4. Pull the agent source

If you already have a local folder for the agent, navigate to it and pull the latest agent definition:

```bash
cd "<agent-folder>"
pac copilot pull
```

This syncs the agent's topics, workflows, knowledge sources, and settings from the Copilot Studio environment into this folder.

### 5. Validate before pushing changes

Before pushing any local edits back up, validate your changes to catch issues early:

1. **Pull first** to make sure you're not overwriting someone else's changes, then check for unexpected diffs:

   ```bash
   pac copilot pull
   git status
   git diff
   ```

2. **Review the diff** of everything you've changed (`topics/`, `workflows/`, `knowledge/`, `settings/`, and the `*.mcs.yml` files) to confirm only intended changes are included.

3. **Confirm authentication** is still pointed at the correct environment:

   ```bash
   pac auth list
   ```

Only proceed to push once the diff looks correct and the YAML is valid.

### 6. Push changes to Copilot Studio

Once validated, push your local changes back to the environment:

```bash
pac copilot push
```

This uploads your local edits to the agent's topics, workflows, knowledge sources, and settings in Copilot Studio.
