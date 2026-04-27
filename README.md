# Ethical-Local-LLM-Workflow
A journey: learning agentic LLM workflows

My goal is to experiment with local development with an eye toward both the environment and ethics. I own an M1 Max MacBook Pro with 32GB memory, which makes running local models more efficient than using a cloud LLM provider.

I chose [StarCoder2-15B-Instruct](https://huggingface.co/bigcode/starcoder2-15b-instruct-v0.1), which is trained on license-filtered open source code (The Stack v2), with documented exclusions and opt out mechanisms. In addition to having far fewer ethical issues than the major cloud LLMs, using it locally avoids many IP risks.

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

Using Microsoft Copilot, I translated it into a set of agents for my own use. See AGENTS.md.
