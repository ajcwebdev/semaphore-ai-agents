# 🚀 Semaphore AI Agents

**An LLM-powered GitHub automation agent** that summarizes commits, flags security issues, and suggests improvements — all integrated into your CI/CD pipeline using [Semaphore](https://semaphoreci.com/).

Built with [Vercel AI SDK](https://sdk.vercel.ai/), [OpenAI GPT-4](https://platform.openai.com/docs/models), and the [GitHub API](https://docs.github.com/en/rest).

---

## ✨ Features

- 🔍 Analyze code changes via GitHub commit diffs
- 🧠 Use GPT-4 to summarize commits and flag issues
- 📄 Generate AI reviews directly in your CI pipeline
- 🔒 Secure with `.env` and Semaphore secrets
- 📦 Modular structure for easy extension and customization

---

## 📁 Project Structure

```bash
semaphore-ai-agents/
├── .semaphore/             # Semaphore pipeline config
├── src/
│   ├── ai/review.ts        # AI agent prompt and analysis logic
│   ├── commits/parser.ts   # Git commit parsing and range detection
│   ├── config.ts           # Environment and runtime configuration
│   └── github/tools.ts     # GitHub API calls to fetch diffs
├── .env.example            # Example environment config
├── package.json
└── index.ts                # Orchestrator: validates config, runs agent
````

---

## 🚀 Getting Started

### 1. Clone the Repo

```bash
git clone https://github.com/ajcwebdev/semaphore-ai-agents.git
cd semaphore-ai-agents
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment

Copy `.env.example` and fill in the required secrets:

```bash
cp .env.example .env
```

```env
OPENAI_API_KEY=your_openai_key
GITHUB_TOKEN=your_github_pat
GITHUB_OWNER=your_github_username
GITHUB_REPO=repo_to_analyze
```

> 💡 GitHub token should have read access to your target repository.

---

## ⚙️ Usage

Run the AI agent locally:

```bash
npx tsx index.ts
```

Or use it as part of a **Semaphore CI pipeline** by including this in your `.semaphore/semaphore.yml`:

```yaml
blocks:
  - name: AI Review
    task:
      jobs:
        - name: Run AI Agent
          commands:
            - checkout
            - npm install
            - npx tsx index.ts
            - cat ai-review.log
```

---

## 🧠 How It Works

1. Fetches commit diff using GitHub API
2. Sends the diff to GPT-4 via Vercel AI SDK
3. Receives AI-powered suggestions and logs the output
4. Artifacts (`ai-review.log`) are stored via Semaphore

---

## 🛡️ Security

* All secrets are loaded via `.env` or Semaphore secret storage.
* Tokens are not logged or exposed.
* Uses minimal permissions for GitHub access.

---

## 🤝 Contributing

We welcome your contributions!

### 🔧 Ideas to Explore

* Add PR title/context to AI prompt
* ESLint or SonarQube integration
* GitLab support
* Web UI for AI feedback

### 🛠 Steps

```bash
# Create a feature branch
git checkout -b your-feature

# Make changes, then:
git commit -m "feat: add your feature"
git push origin your-feature
```

Open a pull request with a clear description and screenshots/logs if needed.


---

## 📚 Resources

* [Semaphore Docs](https://docs.semaphoreci.com/)
* [OpenAI API](https://platform.openai.com/)
* [Vercel AI SDK](https://sdk.vercel.ai/)

