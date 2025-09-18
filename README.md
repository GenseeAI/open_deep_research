# 🔬 Open Deep Research - Enhanced with Gensee Search

> **Fork Notice**: This is an enhanced version of [LangChain's Open Deep Research](https://github.com/langchain-ai/open_deep_research), integrated with [Gensee Search](https://www.gensee.ai/tooling.html) for improved search capabilities and reasoning. Check LangChain's repo to learn more about how it's built.


## 🚀 What's Different in This Version

- **🔍 Gensee Search Integration**: Replaced Tavily with [Gensee Search](https://www.gensee.ai/tooling.html) for enhanced search quality and AI application optimization
- **🧠 Improved Reasoning**: Enhanced agent prompts to encourage more thorough search and reasoning processes
- **🛠️ Easy Integration**: Demonstrates simple integration of Gensee's testing and optimization tools for GenAI applications

*Learn more about Gensee's AI testing and optimization platform at [gensee.ai](https://www.gensee.ai/main.html)*


### 🚀 Quickstart

1. Clone the repository and activate a virtual environment:
```bash
git clone https://github.com/GenseeAI/open_deep_research.git
cd open_deep_research
uv venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

2. Install dependencies:
```bash
uv sync
# or
uv pip install -r pyproject.toml
```

3. Set up your `.env` file to customize the environment variables (for model selection, search tools, and other configuration settings):

Get **FREE** access to Gensee Search from https://platform.gensee.ai/

![Image](https://github.com/user-attachments/assets/bb744cf0-0456-4d2d-b1d6-8c0ba6e76877)

```bash
cp .env.example .env
# GENSEE_API_KEY=your_api_key_here
```

4. Launch agent with the LangGraph server locally:

```bash
# Install dependencies and start the LangGraph server
uvx --refresh --from "langgraph-cli[inmem]" --with-editable . --python 3.11 langgraph dev --allow-blocking
```

This will open the LangGraph Studio UI in your browser.

```
- 🚀 API: http://127.0.0.1:2024
- 🎨 Studio UI: https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024
- 📚 API Docs: http://127.0.0.1:2024/docs
```

Ask a question in the `messages` input field and click `Submit`. Select different configuration in the "Manage Assistants" tab.

### ⚙️ Configurations

See the fields in the [run_evaluate.py](https://github.com/GenseeAI/open_deep_research/blob/main/tests/run_evaluate.py) to config the model usage and other agent behaviors.

### 📊 Evaluation

Open Deep Research is configured for evaluation with [Deep Research Bench](https://huggingface.co/spaces/Ayanami0730/DeepResearch-Leaderboard). This benchmark has 100 PhD-level research tasks (50 English, 50 Chinese), crafted by domain experts across 22 fields (e.g., Science & Tech, Business & Finance) to mirror real-world deep-research needs. It has 2 evaluation metrics, but the leaderboard is based on the RACE score. This uses LLM-as-a-judge (Gemini) to evaluate research reports against a golden set of reports compiled by experts across a set of metrics.

#### Usage

> Warning: Running across the 100 examples can cost ~$20-$100 depending on the model selection.


```bash
# Run comprehensive evaluation on LangSmith datasets
python tests/run_evaluate.py
```

This will provide a link to a LangSmith experiment, which will have a name `YOUR_EXPERIMENT_NAME`. Once this is done, extract the results to a JSONL file that can be submitted to the Deep Research Bench.

```bash
python tests/extract_langsmith_data.py --project-name "YOUR_EXPERIMENT_NAME" --model-name "you-model-name" --dataset-name "deep_research_bench"
```

This creates `tests/expt_results/deep_research_bench_model-name.jsonl` with the required format. Move the generated JSONL file to a local clone of the Deep Research Bench repository and follow their [Quick Start guide](https://github.com/Ayanami0730/deep_research_bench?tab=readme-ov-file#quick-start) for evaluation submission.

#### Results 

| Name | Summarization | Research | Compression | Total Cost | Total Tokens | RACE Score | 
|------|---------------|----------|-------------|------------|--------------|------------|
| Gensee Search | openai:gpt-4.1-mini | openai:gpt-5 | openai:gpt-4.1 | $158.56 | 165,689,034 | 0.5079 |
| LangChain GPT-5 | openai:gpt-4.1-mini | openai:gpt-5 | openai:gpt-4.1 |  | 204,640,896 | 0.4943 |
| LangChain Submission | openai:gpt-4.1-nano | openai:gpt-4.1 | openai:gpt-4.1 | $87.83 | 207,005,549 | 0.4344 |
