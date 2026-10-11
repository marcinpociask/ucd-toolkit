---
name: ucd-figma-connect
description: Figma connection helper of the UCD toolkit. Checks whether Claude can reach Figma and, if not, guides the user step by step through setting up Figma Console MCP (token, MCP server, Desktop Bridge plugin), then verifies the connection and confirms which file is the target. Called by the design blocks (flows, wireframes, hi-fi, audit) whenever work needs Figma, or run on its own. Use for "connect Figma", "set up Figma MCP", "Figma is not connected", "the bridge plugin does not work", "which Figma file are you connected to".
---

# UCD Figma connect

Gets Claude a working, verified connection to the user's Figma file. One step at a time, with a clickable form after each step, so the user never has to read the whole setup guide.

Official setup guide: https://docs.figma-console-mcp.southleft.com/setup. Commands, paths and the troubleshooting table are in `setup-reference.md` in this skill's folder. The tool changes between releases: when a step does not match what the user sees, read the official guide and follow it over this file.

## Rules

- **Never handle the token.** Do not ask the user to paste a Figma token into the chat, and do not type one into a terminal or config file for them. Give the command or config with the placeholder `figd_YOUR_TOKEN_HERE` and have the user run or edit it themselves. If a token appears in the chat anyway, tell the user to revoke it and create a new one.
- **One step per message.** Give the step, then ask the step form. Do not print the next step until the current one is confirmed.
- **Check instead of asking** wherever you can (Node version, config file present, connection status).
- **Never write to a Figma file from this skill.** The write test in step 7 is optional and needs an explicit yes.
- Ask every choice as a clickable form with the AskUserQuestion tool (up to 4 questions, 2-4 options each, recommended option first). If the tool is not available, use numbered options in text.

## 1. Check what is already there

Before any question:

1. Look for Figma tools in the session (loaded or deferred). Typical names: `figma_get_status`, `figma_list_open_files`, `figma_execute` (Figma Console MCP), or the tools of another Figma connector.
2. If Figma Console MCP tools exist, call the status tool with an active probe and list the open files.
3. Go to the matching case:

| Result | Do this |
|---|---|
| Connected and probe succeeds | Skip to step 7 (confirm the target file) |
| Tools exist, no file connected | The server runs but the plugin does not. Start at step 5 |
| Another Figma connector only | Tell the user what it can do. Reading designs and screenshots is enough for an audit. Building flows, wireframes or hi-fi in the file needs write access. Offer the setup below only if the planned work needs more than the connector provides |
| No Figma tools at all | Start at step 2 |

## 2. Intake form

Skip any question the check or the conversation already answered.

| Question | Options | Multi-select |
|---|---|---|
| What do you need Figma for? | Read and audit designs · Create or edit designs · Both | no |
| Which app are you using Claude in? | Claude Code (desktop app, CLI or IDE) · Claude Desktop chat · Claude on the web · Another client (Cursor, Windsurf, VS Code…) | no |
| Is the Figma desktop app installed? | Yes · No, browser only · Not sure | no |
| Do you already have a Figma personal access token? | No, guide me · Yes | no |

Pick the setup mode from the answers and tell the user which one and why:

| Situation | Mode |
|---|---|
| Local client, wants to create or edit, can install Node.js | **NPX** (recommended, full tool set, updates itself) |
| Web client, or cannot install Node.js | **Cloud mode** (pairing code, no Node.js, fewer tools) |
| Only wants to read or evaluate | **Remote read-only** (no plugin needed) |
| Wants to pin a version or contribute | **Local Git** (see the official guide) |

The Figma desktop app is required for every mode that uses the Desktop Bridge plugin. If it is not installed, give the download link (https://www.figma.com/downloads/) as the first step.

## 3. Walk the steps

Exact commands and paths for each step are in `setup-reference.md`. After every step ask the **step form**:

| Question | Options |
|---|---|
| How did that go? | Done · It did not work · I need more detail · Stop here |

On "It did not work", ask what the user sees, match it against the troubleshooting table in `setup-reference.md`, give one fix, and ask the step form again. On "Stop here", say which step to resume from next time.

### NPX mode

| Step | What the user does | What you can check yourself |
|---|---|---|
| 1. Prerequisites | Has Node.js 18 or higher and Figma Desktop | Run `node --version` |
| 2. Token | Creates a personal access token in Figma with the scopes listed in the reference. Copies it once, keeps it private | - |
| 3. Add the server | Runs the one-line command for their client, or edits the client's config file, with their own token in place of the placeholder | After they confirm, check that the server is listed (never print the token) |
| 4. Restart | Fully quits and reopens the client. **This ends the current session.** Before they restart, tell them to run `/ucd-figma-connect` again afterwards; the check in section 1 resumes from the right step | - |
| 5. Import the plugin | In Figma Desktop: Plugins > Development > Import plugin from manifest, and picks the manifest file at the path in the reference | Read the plugin path from the status tool |
| 6. Run the plugin | Opens the design file, runs Plugins > Development > Figma Desktop Bridge, keeps the plugin window open. The status pill should read "ready" | Probe the connection |
| 7. Verify | - | See section 4 |

### Cloud mode

1. Add the cloud endpoint as a custom connector in the client's settings, with the Figma token as the bearer token (the user enters it there, not in chat).
2. Import and run the Desktop Bridge plugin (steps 5 and 6 above).
3. Ask Claude to connect to the plugin; give the user the 6-character pairing code. It is valid for 5 minutes.
4. The user turns on Cloud Mode in the plugin, enters the code and clicks Connect.
5. Verify (section 4).

### Remote read-only

Add the remote endpoint as a custom connector and sign in through the browser prompt. No plugin. State clearly that this mode cannot create or edit anything, then verify by reading a file the user names.

## 4. Verify and confirm the target file

1. Call the status tool with an active probe. Report transport, file name and current page in one line.
2. List the connected files.
3. Ask the **target form**. This matters: people often have a copy, a backup or a library file open, and the plugin connects to whichever file it was last run in.

| Question | Options |
|---|---|
| I am connected to "<file name>", page "<page>". Is this the file to work in? | Yes, this file · No, a different file · I have several files open, let me choose |

- "A different file": the user opens that file and runs the plugin there. Probe again and re-ask.
- Several files: list them by name and let the user pick; lock the target if the tool supports it.

4. Optional write test, only if the planned work creates or edits designs: ask before doing it, create one small frame on a scratch page, screenshot it, delete it.

## 5. Record the connection

If `ux/PROJECT.md` exists, add or update the row in **Design files**: file name, URL, file key, and what the pages contain. Later blocks compare this against the connected file before they write anything.

## 6. Hand back

Say in two or three lines what is connected, in which mode, and what that mode can and cannot do. If another block called this skill, return to it and continue from where it stopped. If the user chose to continue without Figma, say what the calling block will produce instead (written specs, Mermaid diagrams, audit from screenshots).

## Things that go wrong after setup

- **The connection was fine yesterday.** The plugin must be running in the file in every Figma session. Ask the user to run it again, then probe.
- **Wrong file.** Running the plugin in another file can switch the active target. Always state the file name before the first write of a session, and again if the status reports a different file than `ux/PROJECT.md` records.
- **Several Claude sessions open.** Each one starts its own server on the next free port; the plugin connects to all of them. This is normal.
- **Tools missing after an update.** Fully restart the client. If the plugin shows an update banner, re-import the manifest.
