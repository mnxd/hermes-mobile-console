# Hermes Mobile Console

Static mobile-first frontend for Hermes quick operations.

## What Can Be Static

This folder can be deployed to GitHub Pages because it contains only HTML/CSS/JS.

## What Cannot Be Static

Real Hermes operations need the server-side API:

- `/my-assistant/operations/api/mobile_api.py`

The static page calls that API. GitHub Pages must never contain secrets.

## Safe Deployment Model

1. Deploy this folder to GitHub Pages.
2. Run `mobile_api.py` on the server behind HTTPS or a tunnel.
3. Set a strong `HERMES_MOBILE_TOKEN` on the server.
4. In the mobile page, enter API URL and token manually. They are stored only in the phone browser localStorage.

## Server Run Example

```bash
export HERMES_MOBILE_TOKEN='replace-with-long-random-token'
export HERMES_MOBILE_CORS='https://<your-github-user>.github.io'
/usr/local/lib/hermes-agent/venv/bin/uvicorn operations.api.mobile_api:app --host 127.0.0.1 --port 9120
```

Recommended: expose through HTTPS reverse proxy or Cloudflare Tunnel with auth.

## Allowed Commands

- menu / 菜单
- status / 状态
- tasks / 任务
- brief / 简报
- stock / 股票
- courseware / 课件

No arbitrary shell is exposed.
