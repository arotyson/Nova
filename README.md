# Nova English

An English learning app for Tamil speakers: grammar check, 30-day grammar plan, 3-month roadmap, daily words, and AI conversation practice.

Files: `index.html` (the app), `worker.js` (the AI server), `README.md` (this guide).

## Part A: Put the app on GitHub Pages (free)

1. Sign in to github.com, click **New repository**, name it `nova-english`, set **Public**, create it.
2. Click **Add file > Upload files**. Drag in `index.html` and `README.md`. Click **Commit changes**.
   (Do not upload `worker.js` if you want to keep it private. It has no secrets, so uploading is also safe.)
3. Open **Settings > Pages**. Source: **Deploy from a branch**, branch `main`, folder `/ (root)`, **Save**.
4. After about 1 minute your app is at `https://YOUR-USERNAME.github.io/nova-english/`.

Without Part B, only these work: Roadmap, daily checklist, Day 1 lesson, resource links.

## Part B: Make the AI work (Cloudflare Worker + Anthropic API key)

The AI needs a small server so your API key stays secret. Never put the key in `index.html`.

1. Get an API key at console.anthropic.com. API use is billed separately from a Claude subscription. In the Console, set a **low monthly spend limit** first.
2. Sign up at dash.cloudflare.com. Go to **Workers & Pages > Create > Create Worker**. Name it `nova-ai` and click **Deploy**.
3. Click **Edit code**, delete the sample code, paste everything from `worker.js`, then **Deploy**.
4. Open the Worker **Settings > Variables and Secrets** and add:
   - Secret `ANTHROPIC_API_KEY` = your key
   - Variable `ALLOWED_ORIGIN` = `https://YOUR-USERNAME.github.io` (no slash at the end, no `/nova-english`)
5. Copy your Worker URL, like `https://nova-ai.YOURNAME.workers.dev`.

## Part C: Connect the app to the Worker

1. In your GitHub repo, open `index.html` and click the pencil (Edit).
2. Find this line near the top of the script: `const NOVA_API="";`
3. Paste your Worker URL between the quotes, then **Commit changes**.
4. Wait 1 minute and reload your GitHub Pages link. The AI tabs now work.

## Safety notes

- Keep your Worker URL private. Anyone who finds it could use your API credit.
- If the AI stops working, check your spend limit and your API credit in the Anthropic Console.
- Inside Claude, the app works without any of this (it uses Claude directly).
