# Privacy Policy

**Synapse note** · Last updated: 15 November 2026

[🇬🇧 English](PRIVACY.md) · [🇮🇹 Italiano](PRIVACY.it.md)

---

## The short version

**Synapse collects nothing.** No account, no sign-in, no telemetry, no analytics, no crash reporting. Your notes, your attachments and your settings live in a folder on your computer.

There is no Synapse server behind this application. The developer has no way of knowing that you installed it, what you write in it, or whether you use it at all.

Some features send data to third parties **only when you use them**: an online AI engine, a public link, notes and folders shared with other PCs. Each one is described below, with what is sent and where.

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
| Attachments, images, videos | `documenti\` |
| Background images | `sfondi\` |
| Password vaults | `notes.db`, encrypted (see below) |
| API keys for online AI engines | Windows Credential Manager, not the database |
| Error log | `errori.log`, plain text, local only |

None of this is backed up or collected by the developer. If you delete the folder, the data is gone, unless you made a backup yourself or shared a note with someone.

## Password vaults

Vault contents are encrypted with **AES-256-GCM**, using a key derived from your master password with **Argon2id** (64 MB memory, 3 iterations, per-vault salt). A fresh nonce is used for every write.

**Your master password is never stored**, not on disk and not anywhere else. It exists in memory only while a vault is open. This means nobody, including the developer, can recover your secrets if you forget it, and that is the point.

Password vaults are never published, never shared with other PCs, never sent to any AI engine and never included in search.

## When the app uses the network

Synapse works fully offline. Network connections happen **only** in these cases, all of them started by you:

| What you do | Where the request goes | What is sent |
| --- | --- | --- |
| Use the AI assistant with **Ollama** | `127.0.0.1:11434`, Ollama on your own machine | your request and the notes the assistant reads. With a locally downloaded model this never leaves the computer; with an Ollama **cloud** model, Ollama forwards it to its servers (see below) |
| Use the AI assistant with **Claude** | `api.anthropic.com` (Anthropic) | your request, the open note and the notes the assistant reads to answer, with your API key |
| Use the AI assistant with **GPT** | `api.openai.com` (OpenAI) | the same, with your API key |
| Use an **OpenAI-compatible** engine | the address you entered | the same, with your API key if you set one |
| Ask the assistant to search the web | `html.duckduckgo.com` | only the search terms |
| Ask the assistant to read a page, or load an API spec from a URL | the address you or the assistant provide | only the request itself. Addresses on your computer or your local network are refused |
| Open a web page inside a canvas block | the site you open | whatever a normal browser sends: that site can see you, as any site would |
| Create a **public link** | Cloudflare (`*.trycloudflare.com`) | the page of the note you shared, served from your computer (see below) |
| Share notes or folders **with other PCs** | the other PCs, through the iroh network (see below) | the shared notes and their attachments, end-to-end encrypted |
| Download the link program from the setup or the first time you share | `github.com` (Cloudflare's `cloudflared` releases) | only the download request |
| Install Ollama, Python or an AI model from the welcome screen | `ollama.com`, `python.org`, the Ollama model registry | only the download request |

Nothing else. No usage statistics, no "phone home", no update check that carries an identifier. You can verify this with a firewall: block the app entirely and everything except the cases above keeps working.

**Synapse collects nothing in any of these cases.** What a third party does with a request you asked for (an AI provider with your text, DuckDuckGo with your search terms, Cloudflare with a shared page, a website you opened) is governed by that party's own privacy policy.

## The AI assistant

You choose the engine in Settings → *Artificial intelligence*.

**Ollama (default).** Synapse talks to `127.0.0.1:11434`, the Ollama daemon on your own machine. With a model you downloaded and that runs locally, your notes are read locally, the answer is generated locally, and nothing leaves the computer.

> ### ⚠️ Ollama cloud models
>
> Ollama can also serve **cloud models**, which run on Ollama's servers. If you sign in to Ollama and pick one of those, the local daemon forwards your request onward, and with it **the text you sent: your question and the notes the assistant read**.
>
> That connection is made by Ollama, not by Synapse, and it falls under [Ollama's own privacy policy](https://ollama.com/privacy). Cloud models are recognisable by the `-cloud` suffix in their name. If you want the guarantee that nothing leaves your computer, use a model you have downloaded locally (`ollama pull`).

**Claude, GPT or an OpenAI-compatible server.** With one of these engines, your requests, the note you have open and the notes the assistant reads to answer are sent to that provider, using your own API key. The provider processes them under its own terms ([Anthropic](https://www.anthropic.com/legal/privacy), [OpenAI](https://openai.com/policies/privacy-policy)), and usage is billed to your account with them. With an OpenAI-compatible server, the data goes to whoever runs that server: if it runs on your own computer, it doesn't leave it.

Your API keys are stored in the Windows Credential Manager, never in the database, in backups or in shared files. Password vaults are never sent, whatever the engine.

## Public links

The globe in a note publishes a snapshot of that note as a web page. The page is served **from your own computer** while Synapse is open, and reaches the internet through a free Cloudflare tunnel (`cloudflared`, no account). This means:

- whoever has the link can read that page, and Cloudflare carries the traffic between them and your computer;
- the link lasts **10 minutes** from when it was created, then stops working; closing Synapse stops it immediately;
- you can see every open link, and close it, from *Sharing* in the top bar.

## Notes and folders shared with other PCs

When you invite someone into a note or a folder, the two copies of Synapse connect to each other directly, using [iroh](https://iroh.computer). The channel is **end-to-end encrypted** with keys that belong to the two installations.

- There is no Synapse server. When the two networks don't allow a direct connection, traffic passes through a public iroh relay, which forwards encrypted bytes it cannot read or change.
- To let the PCs find each other, while sharing is active each installation's network key and current network addresses are published to iroh's discovery service.
- What travels is only what you shared: the notes, their attachments (up to 100 MB each) and the names you and the other members chose. Password vaults never travel.
- Before anyone joins you see their name and decide. You can change permissions or remove members from *Sharing*.

The other members get a full copy of what you shared, on their own computer, and Synapse cannot take it back from them.

## Children

Synapse is a general-purpose tool and is not directed at children. It does not collect data from anyone, of any age.

## Third parties

Synapse is built with open-source libraries; the full list, with licences, is in the app under Settings → About → *Credits*. Those libraries run locally and none of them send data anywhere except for the features described above.

If you install Ollama, Python or `cloudflared`, or use an online AI provider, those programs and services are governed by their own terms. They are not part of Synapse, and Synapse never sends them anything beyond what you ask it to.

## Distribution

If you installed Synapse from the **Microsoft Store**, Microsoft handles the download and applies its own privacy policy to that transaction. If you downloaded it from **GitHub**, GitHub does the same. Neither passes any personal data on to the developer beyond anonymous download counts.

## Changes to this policy

If this policy changes, the date at the top changes with it, and the previous versions stay visible in this repository's history. There is no mailing list to notify, because there is no list of users.

## Contact

Questions about this policy: open an [issue](../../issues) in this repository.

---

*Synapse holds no personal data on any server, because there is no Synapse server. There is nothing to request access to, nothing to rectify and nothing to erase except the folder on your own computer, which you control entirely.*
