# 📧 Apple Mail Search: Fast & Safe macOS Mail.app Integration

![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-blue) ![Status](https://img.shields.io/badge/Status-Active-green)

## Overview
This skill provides a robust and fast solution for searching and interacting with Apple Mail.app on macOS. Leveraging the `fruitmail` CLI, it offers SQLite-based metadata search and AppleScript integration for full email body content retrieval. Agents can efficiently find messages by various criteria, read their content, and even open them directly in Mail.app.

## Features
-   **Fast Search:** Utilizes SQLite for rapid metadata searches (subject, sender, recipient, date, read status) across large mailboxes, significantly outperforming traditional AppleScript iterations.
-   **Full Body Content:** Retrieve the complete body text of any email using its ID.
-   **Sender-Specific Search:** Easily filter emails by sender's email address or domain.
-   **Unread Mail Listing:** Quickly identify and list all unread messages.
-   **Direct Mail.app Integration:** Open specific emails directly in the Apple Mail.app for manual review or interaction.
-   **Database Statistics:** View statistics about your Mail.app database.
-   **JSON Output:** Option to output search results in JSON format for easy programmatic parsing.
-   **Read-Only Safety:** Operates in a read-only mode to prevent accidental modifications to your mail data; includes an optional `--copy` mode for enhanced safety.
-   **macOS Exclusive:** Designed specifically for Apple Mail.app on macOS.

## Installation
This skill relies on the `fruitmail` CLI, which can be installed via npm:

```bash
npm install -g apple-mail-search-cli
```

## Usage

### Commands
| Command               | Description                                           |
| :-------------------- | :---------------------------------------------------- |
| `fruitmail search`    | Performs complex searches with various filters.       |
| `fruitmail sender <query>` | Searches emails by sender's email.               |
| `fruitmail unread`    | Lists all unread emails.                              |
| `fruitmail body <id>` | Retrieves the full body content of an email by ID.   |
| `fruitmail open <id>` | Opens an email directly in Mail.app by ID.           |
| `fruitmail stats`     | Displays statistics about the Mail.app database.      |

### Search Options
The `fruitmail search` command and other listing commands support the following options:

| Option               | Description                                               |
| :------------------- | :-------------------------------------------------------- |
| `--subject <text>`   | Filters results by text in the subject line.              |
| `--days <n>`         | Limits results to emails received in the last `N` days.   |
| `--unread`           | Shows only unread emails.                                 |
| `--limit <n>`        | Sets the maximum number of results (default: 20).         |
| `--json`             | Outputs results in JSON format.                           |
| `--copy`             | Creates a temporary copy of the Mail database before querying for maximum safety. |

### Examples
```bash
# Find bank statements from the last month
fruitmail search --subject "statement" --days 30

# Get unread emails as JSON and extract subjects
fruitmail unread --json | jq '.[] | .subject'

# Find the 50 most recent emails from Amazon
fruitmail sender "@amazon.com" --limit 50
```

## Configuration
There is no specific configuration required beyond the installation of the `fruitmail` CLI. The tool automatically locates and queries the Apple Mail.app's local database.

## File Structure
This skill typically includes the `SKILL.md` and `_meta.json` files for OpenClaw integration. The core `fruitmail` CLI is managed as an external dependency.

| File          | Description                                                                     |
| :------------ | :------------------------------------------------------------------------------ |
| `SKILL.md`    | OpenClaw skill definition and detailed documentation for using `fruitmail`.     |
| `_meta.json`  | Metadata for the OpenClaw skill, including emoji and tool requirements.         |

> [!NOTE]
> The `_meta.json` file indicates that this skill requires the `fruitmail` binary to be available in the execution environment.

> [!IMPORTANT]
> This skill is **macOS only** and specifically interacts with **Apple Mail.app**. It operates in a **read-only** capacity for searching and reading emails. To compose or send emails, consider using the `himalaya` skill (IMAP/SMTP) or similar tools.
