<div align="center" id="top">
    <img src="frontend\static\gptr-logo2.png" alt="Logo" width="80">
    <p style="
        font-family: 'Georgia', 'Times New Roman', Times, serif;
        color: #2E2D2C;
        font-size: 24px;
        margin-top: 15px;
        text-align: center;
        font-weight: normal;
    ">McMaster Manufacturing Institute (MMRI) <br>Market Data and Trends Analysis Platform</p>

####
<!-- 
[![Website](https://img.shields.io/badge/Official%20Website-gptr.dev-teal?style=for-the-badge&logo=world&logoColor=white&color=0891b2)](https://gptr.dev)
[![Documentation](https://img.shields.io/badge/Documentation-DOCS-f472b6?logo=googledocs&logoColor=white&style=for-the-badge)](https://docs.gptr.dev)
[![Discord Follow](https://dcbadge.vercel.app/api/server/QgZXvJAccX?style=for-the-badge&theme=clean-inverted&?compact=true)](https://discord.gg/QgZXvJAccX)

[![PyPI version](https://img.shields.io/pypi/v/gpt-researcher?logo=pypi&logoColor=white&style=flat)](https://badge.fury.io/py/gpt-researcher)
![GitHub Release](https://img.shields.io/github/v/release/assafelovic/gpt-researcher?style=flat&logo=github)
[![Open In Colab](https://img.shields.io/static/v1?message=Open%20in%20Colab&logo=googlecolab&labelColor=grey&color=yellow&label=%20&style=flat&logoSize=40)](https://colab.research.google.com/github/assafelovic/gpt-researcher/blob/master/docs/docs/examples/pip-run.ipynb)
[![Docker Image Version](https://img.shields.io/docker/v/elestio/gpt-researcher/latest?arch=amd64&style=flat&logo=docker&logoColor=white&color=1D63ED)](https://hub.docker.com/r/gptresearcher/gpt-researcher)
[![Twitter Follow](https://img.shields.io/twitter/follow/assaf_elovic?style=social)](https://twitter.com/assaf_elovic) -->

[English](README.md) | [中文](README-zh_CN.md) | [日本語](README-ja_JP.md) | [한국어](README-ko_KR.md)

</div>

<style>
.md-content {
    font-family: 'Georgia', 'Times New Roman', Times, serif, system-ui;
    color: #2E2D2C;
    font-size: clamp(16px, 2vw, 20px); 
    line-height: 1.6;
}
</style>
<div class="md-content">

## 🔎 GPT Researcher

**GPT Researcher is an open deep research agent designed for both web and local research on any given task.** 

The agent produces detailed, factual, and unbiased research reports with citations. GPT Researcher provides a full suite of customization options to create tailor made and domain specific research agents. Inspired by the recent [Plan-and-Solve](https://arxiv.org/abs/2305.04091) and [RAG](https://arxiv.org/abs/2005.11401) papers, GPT Researcher addresses misinformation, speed, determinism, and reliability by offering stable performance and increased speed through parallelized agent work.

**Our mission is to empower individuals and organizations with accurate, unbiased, and factual information through AI.**

## Why GPT Researcher?

- Objective conclusions for manual research can take weeks, requiring vast resources and time.
- LLMs trained on outdated information can hallucinate, becoming irrelevant for current research tasks.
- Current LLMs have token limitations, insufficient for generating long research reports.
- Limited web sources in existing services lead to misinformation and shallow results.
- Selective web sources can introduce bias into research tasks.

## Architecture

The core idea is to utilize 'planner' and 'execution' agents. The planner generates research questions, while the execution agents gather relevant information. The publisher then aggregates all findings into a comprehensive report.

<div align="center">
<img align="center" height="600" src="https://github.com/assafelovic/gpt-researcher/assets/13554167/4ac896fd-63ab-4b77-9688-ff62aafcc527">
</div>

Steps:
* Create a task-specific agent based on a research query.
* Generate questions that collectively form an objective opinion on the task.
* Use a crawler agent for gathering information for each question.
* Summarize and source-track each resource.
* Filter and aggregate summaries into a final research report.

## ✨ Deep Research

An advanced recursive research workflow that explores topics with agentic depth and breadth. This feature employs a tree-like exploration pattern, diving deeper into subtopics while maintaining a comprehensive view of the research subject.

- 🌳 Tree-like exploration with configurable depth and breadth
- ⚡️ Concurrent processing for faster results
- 🤝 Smart context management across research branches
- ⏱️ Takes ~5 minutes per deep research
- 💰 Costs ~$0.4 per research (using `o3-mini` on "high" reasoning effort)

[Learn more about Deep Research](https://docs.gptr.dev/docs/gpt-researcher/gptr/deep_research) in our documentation.

## ⚙️ Getting Started
### Installation

1. Install Python 3.11 or later. [Guide](https://www.tutorialsteacher.com/python/install-python).
2. Clone the project and navigate to the directory:

  ```cmd
  git clone https://github.com/Guann-Ahiramei/industry_reportor.git
  cd gpt-researcher
  ```

3. Set up API keys by exporting them or storing them in a `.env` file.

  ```.env
  OPENAI_API_KEY={Your OpenAI API Key here}
  TAVILY_API_KEY={Your Tavily API Key here}
  ```

4. If you need to use searching locally or hybrid, add the following to your `.env` file:

  First,install [ollama](https://ollama.ai/) and pull the models, run the following command:
  ```.cmd
  ollama pull nomic-embed-text
  ollama pull llama3.2:latest
  ```

  Then, add the following to your `.env` file:

  ```.env
  DOC_PATH=./my-docs
  OLLAMA_BASE_URL="http://127.0.0.1:11434/"
  FAST_LLM="ollama:llama3.2:latest"
  SMART_LLM="ollama:llama3.2:latest"
  STRATEGIC_LLM="ollama:llama3.2:latest"
  EMBEDDING="ollama:nomic-embed-text"
  ```  

5. Create a virtual environment and activate it: (optional)

  ```cmd
  python -m venv gptr-env
  .\gptr-env\Scripts\activate
  ```

6.  Install dependencies and start the server:

    ```cmd
    pip install -r requirements.txt
    python -m uvicorn main:app --reload
    ```

Visit [http://127.0.0.1:8000](http://127.0.0.1:8000) to start.

## Run as PIP package
```cmd
pip install gpt-researcher

```
### Example Usage:
```python
...
from gpt_researcher import GPTResearcher

query = "what is the Technology Adoption trend of canada aerospace industry?"
researcher = GPTResearcher(query=query, report_type="research_report")
# Conduct research on the given query
research_result = await researcher.conduct_research()
# Write the report
report = await researcher.write_report()
...
```

**For more examples and configurations, please refer to the [PIP documentation](https://docs.gptr.dev/docs/gpt-researcher/gptr/pip-package) page.**

## 📄 Research on Local Documents

You can instruct the GPT Researcher to run research tasks based on your local documents. Currently supported file formats are: PDF, plain text, CSV, Excel, Markdown, PowerPoint, and Word documents.

Step 1: Add the env variable `DOC_PATH` pointing to the folder where your documents are located.

```.env
DOC_PATH="./my-docs"
```

Step 2: 
 - If you're running GPT Researcher with the [PIP package](https://docs.tavily.com/guides/gpt-researcher/gpt-researcher#pip-package), pass the `report_source` argument as "local" when you instantiate the `GPTResearcher` class [code sample here](https://docs.gptr.dev/docs/gpt-researcher/context/tailored-research).

## 📖 Documentation

This project is forked from [GPT-Researcher](https://github.com/assafelovic/gpt-researcher). For more information, please refer to the original [documentation](https://docs.gptr.dev/docs/gpt-researcher/getting-started/getting-started) for:
- Installation and setup guides
- Configuration and customization options
- How-To examples
- Full API references

## Demo
https://github.com/user-attachments/assets/2cc38f6a-9f66-4644-9e69-a46c40e296d4

## Tutorials
 - [How it Works](https://docs.gptr.dev/blog/building-gpt-researcher)
 - [How to Install](https://www.loom.com/share/04ebffb6ed2a4520a27c3e3addcdde20?sid=da1848e8-b1f1-42d1-93c3-5b0b9c3b24ea)
 - [Live Demo](https://www.loom.com/share/6a3385db4e8747a1913dd85a7834846f?sid=a740fd5b-2aa3-457e-8fb7-86976f59f9b8)

## 🛡 Disclaimer

This project, GPT Researcher, is an experimental application and is provided "as-is" without any warranty, express or implied. We are sharing codes for academic purposes under the Apache 2 license. Nothing herein is academic advice, and NOT a recommendation to use in academic or research papers.

Our view on unbiased research claims:
1. The main goal of GPT Researcher is to reduce incorrect and biased facts. How? We assume that the more sites we scrape the less chances of incorrect data. By scraping multiple sites per research, and choosing the most frequent information, the chances that they are all wrong is extremely low.
2. We do not aim to eliminate biases; we aim to reduce it as much as possible. **We are here as a community to figure out the most effective human/llm interactions.**
3. In research, people also tend towards biases as most have already opinions on the topics they research about. This tool scrapes many opinions and will evenly explain diverse views that a biased person would never have read.

---
</div>


<p align="right">
  <a href="#top">⬆️ Back to Top</a>
</p>
