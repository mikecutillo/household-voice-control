# Household Voice Control

A voice-interface layer that bridges Amazon Alexa (and, in progress, other assistants) to a local AI Operating System — so a household voice command can trigger anything in AIOS instead of being limited to the vendor's walled garden of skills.

> *This repo is a public overview. The running code is private.*

---

## What it is

Consumer voice assistants are siloed — Alexa talks to Alexa things, Siri talks to Apple things, Google talks to Google things. This project replaces that with a single passthrough layer: voice commands hit a custom skill, which forwards the intent to a local webhook running inside AIOS. From there, any connected service — lights, Discord posts, Notion writes, AI queries — becomes voice-addressable.

## What it does

- **Custom Alexa Skill** that captures arbitrary spoken intents and forwards them to AIOS
- **Webhook router** inside AIOS that parses intent, resolves the target capability, and executes
- **Natural-language fallback** — if no explicit intent matches, the raw utterance is sent to Claude for interpretation and command generation
- **Response synthesis** — AIOS composes a spoken reply and hands it back to Alexa for TTS
- **Device control bridge** — ties into local Hue lights, router SOAP API, and curfew/device state

## Software

| Layer | Tech |
|---|---|
| Voice frontend | Amazon Alexa Skills Kit, custom skill with open-ended slots |
| Cloud bridge | AWS Lambda (TypeScript) |
| Local bridge | AIOS webhook endpoint (Next.js API route) |
| Intent reasoning | Anthropic Claude for fallback parsing and response generation |
| Device layer | Philips Hue API, router SOAP, Discord webhooks |

## What this demonstrates

- **Vendor-neutral voice architecture** — the voice stack is a transport, not a lock-in
- **LLM-as-parser** — leaning on Claude to handle the long tail of natural commands that rigid slot templates can't express
- **Bidirectional flow** — voice → local AI → connected device → spoken confirmation, all round-tripping cleanly

## Stack

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![AWS Lambda](https://img.shields.io/badge/AWS_Lambda-FF9900?style=flat&logo=awslambda&logoColor=white)
![Alexa](https://img.shields.io/badge/Alexa-00CAFF?style=flat&logo=amazonalexa&logoColor=white)
![Anthropic Claude](https://img.shields.io/badge/Anthropic_Claude-CC785C?style=flat&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)

---

Part of the AIOS portfolio. See the [profile README](https://github.com/mikecutillo) for the full system map.
