# rag-demystified

Questions that span several documents need more than a single similarity search. rag-demystified is a Python application that makes an LLM-based retrieval-augmented generation (RAG) pipeline easier to inspect: it breaks questions into sub-questions, retrieves context from city Wikipedia articles, and combines the answers.

## Features

- Break complex questions into sub-questions, with a data source and retrieval method selected for each.
- Retrieve relevant document chunks through EvaDB's FAISS vector index for focused questions.
- Use an entire source document as context for summary questions, provided it fits within the LLM context limit.
- Combine sub-question responses into a final answer through an LLM call.
- Expose the prompt-template, context, and question pattern behind the pipeline's LLM calls.

## Installation

From the project directory, install the Python dependencies. A Python environment with `pip` is required; a virtual environment is recommended.

```sh
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

On Windows, activate the environment with `.venv\Scripts\activate` instead.

**An OpenAI API key is required.** Create the local configuration file, replacing `yourkey` with your key:

```sh
echo OPENAI_API_KEY='yourkey' > .env
```

This command overwrites an existing `.env` file. Keep the file out of version control. OpenAI API calls may incur charges.

## Usage

Run the application from the project directory:

```sh
python complex_qa.py
```

The example uses a collection of Wikipedia articles, with each city treated as a separate data source. Questions for this setup include:

- "What is the population of Chicago?"
- "Give me a summary of the positive aspects of Atlanta."
- "Which city has the highest population?"

A focused question can use vector retrieval to select relevant chunks. A summary question can use the full source document. A comparison across cities requires sub-questions over multiple sources, followed by response aggregation.

The example limits document size to fit within the LLM context window. Answers depend on the supplied articles, the retrieval results, and the model's responses; check the source material before relying on factual comparisons.

## License

Licensed under Apache-2.0. This project is based on [pchunduri6/rag-demystified](https://github.com/pchunduri6/rag-demystified). Retain the upstream license and applicable copyright and attribution notices when redistributing it.
