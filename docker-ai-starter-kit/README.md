# Docker AI starter kit (by the n8n team)

**Docker AI Starter Kit** is an open Docker Compose template that quickly bootstraps 
a fully featured local AI and Low Code development environment, including an Open WebUI 
for the communication interface (chat) with your local LLMs.

This is the version with the addition of **Open WebUI**. 
[Original **Self-hosted AI starter kit**](https://github.com/n8n-io/self-hosted-ai-starter-kit)

![n8n.io - Screenshot](https://raw.githubusercontent.com/n8n-io/self-hosted-ai-starter-kit/main/assets/n8n-demo.gif)

Curated by <https://github.com/n8n-io> and <https://github.com/Alexsashkin>, 
it combines the self-hosted n8n platform with a curated list of compatible AI 
products and components to quickly get started with building self-hosted AI workflows.

### What’s included

✅ [**Self-hosted n8n**](https://n8n.io/) - Low-code platform with over 400
integrations and advanced AI components

✅ [**Ollama**](https://ollama.com/) - Cross-platform LLM platform to install
and run the latest local LLMs

✅ [**Qdrant**](https://qdrant.tech/) - Open-source, high performance vector
store with an comprehensive API

✅ [**PostgreSQL**](https://www.postgresql.org/) -  Workhorse of the Data
Engineering world, handles large amounts of data safely.

✅ [**pgAdmin**](https://www.pgadmin.org/) - Open-source administration and development platform for PostgreSQL.

✅ [**Open WebUI**](https://openwebui.com/) - A chat interface (similar to ChatGPT) 
for private communication with your local LLMs.

✅ [**Selenium**](https://www.selenium.dev/) - Selenium automates browsers.

✅ [**Flaresolverf**](https://flaresolverr.com/) - Web Scraping.

## Installation

### Cloning the Repository

```bash
git clone https://github.com/Alexsashkin/ai-agents.git
cd ai-agents/docker-ai-starter-kit
```

### Running n8n using Docker Compose

#### For Nvidia GPU users

```
docker compose --profile gpu-nvidia up
```

> [!NOTE]
> If you have not used your Nvidia GPU with Docker before, please follow the
> [Ollama Docker instructions](https://github.com/ollama/ollama/blob/main/docs/docker.md).

### For AMD GPU users on Linux

```
docker compose --profile gpu-amd up
```

#### For Mac / Apple Silicon users

If you’re using a Mac with an M1 or newer processor, you can't expose your GPU
to the Docker instance, unfortunately. There are two options in this case:

1. Run the starter kit fully on CPU, like in the section "For everyone else"
   below
2. Run Ollama on your Mac for faster inference, and connect to that from the
   n8n instance

If you want to run Ollama on your mac, check the
[Ollama homepage](https://ollama.com/)
for installation instructions, and run the starter kit as follows:

```
docker compose up
```

##### For Mac users running OLLAMA locally

If you're running OLLAMA locally on your Mac (not in Docker), you need to modify 
the OLLAMA_HOST environment variable in the n8n service configuration. 
Update the x-n8n section in your Docker Compose file as follows:

```yaml
x-n8n: &service-n8n
  # ... other configurations ...
  environment:
    # ... other environment variables ...
    - OLLAMA_HOST=host.docker.internal:11434
```

Additionally, after you see "Editor is now accessible via: <http://localhost:5678/>":

1. Head to <http://localhost:5678/home/credentials>
2. Click on "Local Ollama service"
3. Change the base URL to "http://host.docker.internal:11434/"

#### For everyone else

```
docker compose --profile cpu up
```

## ⚡️ Quick start and usage

The core of the Docker AI Starter Kit is a Docker Compose file, pre-configured with network and storage settings, 
minimizing the need for additional installations.
After completing the installation steps above, simply follow the steps below to get started.

1. Open <http://localhost:5678/> in your browser to set up n8n. You’ll only
   have to do this once. You are **NOT** creating an account with n8n in the setup here, 
   it is only a local account for your instance!

2. Create credentials for every service:
   
   **Ollama URL**: http://localhost:11434

   **Postgres**: use DB, username, and password from n8n/.env. Host is postgres

   **Qdrant URL**: http://localhost:6333 (API key can be whatever since this is running locally)

   **Google Drive**: Follow [this guide from n8n](https://docs.n8n.io/integrations/builtin/credentials/google/).
   Don't use localhost for the redirect URI, just use another domain you have, it will still work!
   Alternatively, you can set up [local file triggers](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.localfiletrigger/).

3. If this is the first time you’re running the workflow, you may need to wait
   until Ollama finishes downloading Llama3.2. You can inspect the docker
   console logs to check on the progress.

4. Open <http://localhost:3000/> in your browser to set up Open WebUI. You’ll 
   only have to do this once. You are **NOT** creating an account with Open WebUI 
   in the setup here, it is only a local account for your instance!

### To use

* **n8n**: visit <http://localhost:5678/> in your browser.

* **Open WebUI**: visit <http://localhost:3000/> in your browser.

* **Qdrant Dashboard**: visit http://localhost:6333/dashboard in your browser.

* **pgAdmin**: visit http://localhost:8080/ in your browser.

* **Selenium Grid**: visit http://localhost:4444/ui/ in your browser.


With your n8n instance, you’ll have access to over 400 integrations and a
suite of basic and advanced AI nodes such as
[AI Agent](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/),
[Text classifier](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.text-classifier/),
and [Information Extractor](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.information-extractor/)
nodes. To keep everything local, just remember to use the Ollama node for your
language model and Qdrant as your vector store.

> [!NOTE]
> This starter kit is designed to help you get started with self-hosted AI
> workflows. While it’s not fully optimized for production environments, it
> combines robust components that work well together for proof-of-concept
> projects. You can customize it to meet your specific needs

## Upgrading

* ### For Nvidia GPU setups:

```bash
docker compose --profile gpu-nvidia pull
docker compose create && docker compose --profile gpu-nvidia up
```

* ### For Mac / Apple Silicon users

```
docker compose pull
docker compose create && docker compose up
```

* ### For Non-GPU setups:

```bash
docker compose --profile cpu pull
docker compose create && docker compose --profile cpu up
```

## 👓 Recommended reading

n8n is full of useful content for getting started quickly with its AI concepts
and nodes. If you run into an issue, go to [support](#support).

- [AI agents for developers: from theory to practice with n8n](https://blog.n8n.io/ai-agents/)
- [Tutorial: Build an AI workflow in n8n](https://docs.n8n.io/advanced-ai/intro-tutorial/)
- [Langchain Concepts in n8n](https://docs.n8n.io/advanced-ai/langchain/langchain-n8n/)
- [Demonstration of key differences between agents and chains](https://docs.n8n.io/advanced-ai/examples/agent-chain-comparison/)
- [What are vector databases?](https://docs.n8n.io/advanced-ai/examples/understand-vector-databases/)

## 🎥 Video walkthrough

- [Installing and using Local AI for n8n](https://www.youtube.com/watch?v=xz_X2N-hPg0)

## 🛍️ More AI templates

For more AI workflow ideas, visit the [**official n8n AI template
gallery**](https://n8n.io/workflows/categories/ai/). From each workflow,
select the **Use workflow** button to automatically import the workflow into
your local n8n instance.

### Learn AI key concepts

- [AI Agent Chat](https://n8n.io/workflows/1954-ai-agent-chat/)
- [AI chat with any data source (using the n8n workflow too)](https://n8n.io/workflows/2026-ai-chat-with-any-data-source-using-the-n8n-workflow-tool/)
- [Chat with OpenAI Assistant (by adding a memory)](https://n8n.io/workflows/2098-chat-with-openai-assistant-by-adding-a-memory/)
- [Use an open-source LLM (via Hugging Face)](https://n8n.io/workflows/1980-use-an-open-source-llm-via-huggingface/)
- [Chat with PDF docs using AI (quoting sources)](https://n8n.io/workflows/2165-chat-with-pdf-docs-using-ai-quoting-sources/)
- [AI agent that can scrape webpages](https://n8n.io/workflows/2006-ai-agent-that-can-scrape-webpages/)

### Local AI templates

- [Tax Code Assistant](https://n8n.io/workflows/2341-build-a-tax-code-assistant-with-qdrant-mistralai-and-openai/)
- [Breakdown Documents into Study Notes with MistralAI and Qdrant](https://n8n.io/workflows/2339-breakdown-documents-into-study-notes-using-templating-mistralai-and-qdrant/)
- [Financial Documents Assistant using Qdrant and](https://n8n.io/workflows/2335-build-a-financial-documents-assistant-using-qdrant-and-mistralai/) [Mistral.ai](http://mistral.ai/)
- [Recipe Recommendations with Qdrant and Mistral](https://n8n.io/workflows/2333-recipe-recommendations-with-qdrant-and-mistral/)

## Tips & tricks

### Accessing local files

The self-hosted AI starter kit will create a shared folder (by default,
located in the same directory) which is mounted to the n8n container and
allows n8n to access files on disk. This folder within the n8n container is
located at `/data/shared` -- this is the path you’ll need to use in nodes that
interact with the local filesystem.

**Nodes that interact with the local filesystem**

- [Read/Write Files from Disk](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.filesreadwrite/)
- [Local File Trigger](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.localfiletrigger/)
- [Execute Command](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.executecommand/)

## 📜 License

This project ([originally **Self-hosted AI starter kit** created by the n8n team](https://github.com/n8n-io/self-hosted-ai-starter-kit)) 
is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.
