# Privacy Policy

**Synapse note** · Last updated: 6 August 2026

[🇬🇧 English](PRIVACY.md) · [🇮🇹 Italiano](PRIVACY.it.md)

---

## The short version

**Synapse collects nothing.** No account, no sign-in, no telemetry, no analytics, no crash reporting. Your notes, your attachments and your settings live in a folder on your computer and are never sent anywhere.

There is no server behind this application. The developer has no way of knowing that you installed it, what you write in it, or whether you use it at all.

---

## What data the app holds, and where

Everything Synapse stores lives on your own machine, by default in:

```
C:\Users\<you>\.synapse
```

You can move that folder anywhere from Settings → *Data and backup*.

| What | Where |
| --- | --- |
| Notes, folders, settings | `notes.db`, a standard SQLite file |
| Attachments and images | `documenti\` |
| Background images | `sfondi\` |
| Password vaults | `notes.db`, encrypted (see below) |
| Error log | `errori.log`, plain text, local only |

None of this is transmitted, synced or backed up by us. If you delete the folder, the data is gone — there is no copy anywhere else.

## Password vaults

Vault contents are encrypted with **AES-256-GCM**, using a key derived from your master password with **Argon2id** (64 MB memory, 3 iterations, per-vault salt). A fresh nonce is used for every write.

**Your master password is never stored**, not on disk and not anywhere else. It exists in memory only while a vault is open. This means nobody — including the developer — can recover your secrets if you forget it, and that is the point.

## When the app uses the network

Synapse works fully offline. Network connections happen **only** in these cases, all of them started by you:

| What you do | Where the request goes | What is sent |
| --- | --- | --- |
| Use the AI assistant | `127.0.0.1:11434` — [Ollama](https://ollama.com) on your own machine | your prompt and the note you have open; it does not leave the computer |
| Ask the assistant to search the web | `html.duckduckgo.com` | only the search terms |
| Ask the assistant to read a page, or load an API spec from a URL | the address you provide | only the request itself |
| Open a web page inside a canvas block | the site you open | whatever a normal browser sends: that site can see you, as any site would |
| Install Ollama or Python from the welcome screen | `ollama.com`, `python.org` | only the download request |

Nothing else. No usage statistics, no "phone home", no update check that carries an identifier. You can verify this with a firewall: block the app entirely and everything except the cases above keeps working.

## The AI assistant

The assistant runs **on your computer**, through Ollama, with a model you downloaded yourself. Your notes are read locally and the answers are generated locally. No prompt and no note is sent to the developer or to any AI provider.

The two exceptions are the ones listed above: web search, which sends only your search terms to DuckDuckGo, and reading a web page, which fetches the address you asked for.

## Children

Synapse is a general-purpose tool and is not directed at children. It does not collect data from anyone, of any age.

## Third parties

Synapse is built with open-source libraries; the full list, with licences, is in the app under Settings → About → *Credits*. Those libraries run locally and none of them send data anywhere.

If you install Ollama or Python, those programs are governed by their own terms — they are not part of Synapse, and Synapse never sends them anything beyond what you ask it to.

## Distribution

If you installed Synapse from the **Microsoft Store**, Microsoft handles the download and applies its own privacy policy to that transaction. If you downloaded it from **GitHub**, GitHub does the same. Neither passes any personal data on to the developer beyond anonymous download counts.

## Changes to this policy

If this policy changes, the date at the top changes with it, and the previous versions stay visible in this repository's history. There is no mailing list to notify, because there is no list of users.

## Contact

Questions about this policy: open an [issue](../../issues) in this repository.

---

*Synapse holds no personal data on any server, because there is no server. There is nothing to request access to, nothing to rectify and nothing to erase except the folder on your own computer, which you control entirely.*
