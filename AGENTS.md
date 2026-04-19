Project: Omniflow

## What We're Building
An AI-native workflow automation platform. Users describe what they 
want in plain English, an overarching AI generates a visual pipeline 
of blocks, and those blocks execute using the user's own AI 
subscriptions (Claude, Codex, GPT etc). Built on top of the 
Open Agents fork with n8n as the execution engine underneath.

## Tech Stack
- Framework: Next.js (from Open Agents fork)
- Database: Supabase (Postgres)
- Execution engine: Self-hosted n8n (private API, users never see it)
- Pipeline canvas: React Flow
- Auth: Already in Open Agents (Vercel OAuth + GitHub)
- Payments: Stripe (not in v1)
- Desktop companion: Electron or Tauri (not in v1)
- Language: TypeScript throughout

## Architecture
Web canvas → Overarching AI → Pipeline JSON → n8n execution engine
Each block has its own AI model assigned (user's own API keys/subscriptions)
Companion agent (local daemon) handles CLI bridges to Claude Code/Codex
Blocks communicate via standardised JSON envelope

## V1 Scope — Build Only These
1. Pipeline generator (plain English → pipeline JSON via Claude)
2. Visual canvas (React Flow, view and edit pipelines)
3. Block system (14 block types — see below)
4. Credential vault (encrypted API keys + OAuth tokens)
5. Cron scheduler (per pipeline, not per block)
6. Run history and live trace
7. Dry run mode
8. User dashboard

## V1 Block Types
Chat/Reason, Code, Web Search, File Read, File Write, 
HTTP Request, Google Sheets, Gmail, Telegram, Slack, 
Condition, Transform, Trigger, Notify

## Not In V1 — Do Not Build These
- White labelling
- Team/multi-user workspaces  
- Workflow marketplace
- Mobile app
- Per-block scheduling
- Monaco code editor
- Voice input

## Coding Conventions
- TypeScript strict mode always
- Functional components, no class components
- Server components by default, client components only when needed
- All API routes in /app/api
- All block logic in /packages/blocks
- Environment variables via .env.local only, never hardcoded
- Error handling: try/catch on every async operation, log to console in dev
- Commit after every working feature, never commit broken code

## Current Priority
Build the pipeline generator first as a standalone proof of concept.
Input: plain English description
Output: valid pipeline JSON with blocks and connections
This must work reliably before building any UI.
