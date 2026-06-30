# Project-02-AI-Email-Responder
## Overview

This n8n workflow takes an incoming email (sender, subject, body)
and uses the Claude API to draft a warm, professional reply ready
for human review before sending.

## Problem It Solves

Responding to inquiry emails takes time and mental energy —
especially repetitive ones like "what do you charge, how does this
work." This automation drafts a strong starting reply in seconds,
so the human only needs to review and personalize before sending,
not write from scratch.

## How It Works

1. Email data (sender name, subject, body) is set manually for
testing — designed to later connect to a real inbox trigger
2. n8n sends the email content to Claude with instructions to draft
a warm, professional, concise reply under 150 words
3. Claude returns a complete draft, signed off as "MELON AI Team"
4. The draft is cleaned and ready to review

## Tech Stack

- n8n (VPS-hosted, accessed via SSH tunnel)
- Claude API (claude-sonnet-4-6)
- HTTP Request node with Header Auth credential

## Workflow Diagram

!Screenshot 2026-06-30 072943.png

!Screenshot 2026-06-30 072848.png

## Setup Instructions

1. Import workflow JSON into n8n
2. Use existing "Claude API" Header Auth credential
(x-api-key set to Anthropic API key)
3. Ensure Headers include both anthropic-version (2023-06-01)
and content-type (application/json)
4. Edit the Set node with real sender/subject/body data
5. Click Test Workflow

## Test Case Used

Simulated inquiry from "Sarah," a bakery owner asking about
Instagram automation services and pricing

## Results

**Test Input:**

- From: Sarah
- Subject: Question about your automation services
- Message: "Hi, I saw your post about AI automations. Do you build
custom workflows for small businesses? I run a local bakery and
want to automate my Instagram posting. What would that cost and
how long would it take?"

**Claude's Drafted Reply:**

Subject: Re: Question about your automation services

Hi Sarah,

Thanks so much for reaching out — and what a sweet business to be
running! 🍰

Yes, we absolutely build custom AI workflows for small businesses,
and automating Instagram posting is a great place to start.

For a solution like yours, we'd typically build a workflow that can
auto-generate captions, schedule posts, and even pull from your
product photos — saving you hours each week.

In terms of cost and timeline, it really depends on your specific
needs, but most small business projects like this are affordable
and quick to implement (often within 1–2 weeks).

We'd love to hop on a quick discovery call to give you an accurate
quote. Are you free for a 20-minute chat this week?

Looking forward to hearing from you!

Warm regards,
MELON AI Team

## AI Limitations Observed

- Claude used markdown formatting (bold asterisks) that would need
conversion before going into a real email client
- Claude confidently stated specifics it was never given — a
"1-2 week" timeline and "affordable" pricing language — neither
of which were provided in the prompt. This is a clear example of
why human review before sending is mandatory, not optional, in
any client-facing AI automation.

## Lessons Learned

- Forgot the anthropic-version header when building this node fresh
— confirmed this header is required on every HTTP Request node
calling the Anthropic API, not just the first one
- AI output quality was strong on tone and structure, but needs
guardrails (real pricing/timeline data, or explicit instruction
to stay vague) before being client-ready
- This workflow's pattern (structured input → AI draft → human
review) is the actual sellable product, not just a demo

## Content Created From This

- [ ]  YouTube video (Video 4 — AI Email Responder build)
- [x]  GitHub repository
- [x]  LinkedIn post
- [x]  X post
- [x]  Instagram post

## Date Built

[6/30/2026]

## Status

Complete (manual trigger version) — real inbox integration is a
future upgrade
