# Ethical-Local-LLM-Workflow
A journey: learning agentic LLM workflows

My goal is to experiment with local development with an eye toward both the environment and ethics. I own an M1 Max MacBook Pro with 32GB memory, which makes running local models more efficient than using a cloud LLM provider.

I chose [StarCoder2-15B-Instruct](https://huggingface.co/bigcode/starcoder2-15b-instruct-v0.1), which is trained on license-filtered open source code (The Stack v2), with documented exclusions and opt out mechanisms. In addition to having far fewer ethical issues than the major cloud LLMs, using it locally avoids many IP risks. (I don't yet know if my computer can handle the 15B model; I may need to drop down to the 7B model.)

I was inspired to do this project by a [LinkedIn post by David Jorjani](https://www.linkedin.com/posts/jorjani_a-few-weeks-ago-i-taught-a-bonus-lecture-share-7452379429445668865-V6nK) that chronicled his 50-minute lecture on AI where he designed, built, tested, and deployed 3 new real, live product features using a series of AI agents.

Here is David's workflow, copied and pasted from that article:

1) Understand: The user described their experience in plain language. Claude and I translated those into specifications, mapping them against expectations and existing code. That became 6 separate feature requests.

2) Estimate: I did quick estimates of the complexity of each one (XS/S/M/L/XL). We had 50 minutes and wanted to get it right. Time budget is the most serious constraint vibe coders overlook. This is where I follow Basecamp's Shape Up methodology.

3) Prioritize: I had Claude score all 6 features by difficulty and impact. We estimated we could get 3 out of 6 done. We could ship confidently.

4) Scope: Simply said, how do we know it's done? What should be done? What should not be done? Bonus is that this work makes the code more testable. If we don't specify, agents will have to make things up (aka hallucinate). Then we complain.

5) Prototype: This helps us get on the same page. This first pass caught clinically inaccurate labels.

6) Build: I delegated each feature to a specialized sub-agent that wrote the code.

7) Review: I ran separate review agents to check for bugs, clinical accuracy, and code quality. First pass caught dead code and a math issue that could cause a visual glitch. All fixed. I validated every change. Second pass: clean.

8) Ship: 9 tests to verify before it goes live. Automated checks passed.

Using Microsoft Copilot, I translated it into a set of agents for my own use. See AGENTS.md. This file will evolve as I tune the agents.

# Installation

## 1. Install Homebrew (Package Manager)
Homebrew makes it easy to install and manage command-line tools. If you already have Homebrew, skip to step 2.

```bash/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"```

After installation, verify it worked:

```bashbrew --version```

## 2. Install Ollama

Ollama is the runtime that lets you run large language models locally on your machine.

```brew install ollama```

Start the Ollama service:

```brew services start ollama```

Verify Ollama is running (from another terminal):

```ollama --version```

## 3. Pull the StarCoder2-15B-Instruct Model

Now you'll download the StarCoder2 model to your local machine. This is a one-time process that may take 10-30 minutes depending on your internet speed (the model is ~9GB).

```ollama pull starcoder2:15b-instruct```

Once complete, verify the model is installed:

```ollama list```

You should see `starcoder2:15b-instruct` in the list.

Test the model locally:

```ollama run starcoder2:15b-instruct "Write a Python function that returns hello world"```

## 4. Install the Continue VS Code Extension

Continue is an open-source AI code assistant that integrates directly into VS Code. It will use your local Ollama model.

1. Open VS Code
2. Click the Extensions icon (left sidebar, looks like 4 squares)
3. Search for "Continue"
4. Click the blue "Install" button for the "Continue" extension by Continue.dev
5. Reload VS Code when prompted

## Useful commands

```
# Check if Ollama is running
brew services list

# View all installed models
ollama list

# Run the model interactively
ollama run starcoder2:15b-instruct

# Stop Ollama
brew services stop ollama

# Restart Ollama (fixes most issues)
brew services restart ollama
```
