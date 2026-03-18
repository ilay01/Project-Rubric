# Document Assistant Project

Build a multi-agent document assistant using LangChain and LangGraph.
The assistant can classify user intent, retrieve financial and healthcare documents,
summarize content, and run calculations using tools.

## Project Goal

You will complete TODO sections across the codebase to implement:

1. Structured schemas for agent outputs
2. Intent-based routing in a LangGraph workflow
3. Specialized agent nodes for Q&A, summarization, and calculation
4. Memory updates and state persistence
5. Prompt selection by intent
6. A safe calculator tool with logging

## Getting Started

### Prerequisites

- Python 3.9+
- OpenAI API key
- pip and virtual environment support

### Installation

1. Open a terminal in `project`
2. Create and activate a virtual environment
3. Install dependencies
4. Configure environment variables

```bash
cd project
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Create a `.env` file in `project` with:

```bash
# OpenAI API Configuration
OPENAI_API_KEY=
# Optional: Model Configuration
MODEL_NAME=gpt-4o
TEMPERATURE=0.1

# Optional: Session Storage
SESSION_STORAGE_PATH=./sessions
```

## Dependencies

The project uses the packages listed in `requirements.txt`, including:

- langchain
- langgraph
- langchain-openai
- langchain-core
- pydantic
- python-dotenv
- openai
- print-color

## Running the Assistant

From `project`:

```bash
python main.py
```

Available runtime commands:

- `/help`
- `/docs`
- `/quit`

## Project Structure

```text
project/
├── main.py
├── requirements.txt
├── README.md
├── docs/
├── logs/
├── sessions/
└── src/
	 ├── schemas.py
	 ├── retrieval.py
	 ├── tools.py
	 ├── prompts.py
	 ├── agent.py
	 └── assistant.py
```

## Student Tasks

### 1. Schemas in `src/schemas.py`

Implement:

- `AnswerResponse`
- `UserIntent`

### 2. Agent State and Workflow in `src/agent.py` and `src/assistant.py`

Implement and verify:

1. Intent classification node
2. Summarization and calculation agent nodes
3. Memory update node
4. Workflow assembly and routing
5. Checkpointer integration using `InMemorySaver`
6. Configurable workflow values in `process_message`:
   - `thread_id`
   - `llm`
   - `tools`

### 3. Prompt Logic in `src/prompts.py`

Implement:

1. Intent-based prompt selection in `get_chat_prompt_template`
2. Calculation system prompt that forces calculator tool use for every computation

### 4. Tools in `src/tools.py`

Implement:

- `create_calculator_tool` with:
  - tool decorator
  - expression validation
  - safe eval usage
  - logging
  - formatted output
  - error handling

## Testing Guidance

Use a mix of manual and automated checks.

### Suggested Manual Tests

1. Q&A request:
   - Ask for invoice or contract facts
2. Summarization request:
   - Ask for summary of one or more docs
3. Calculation request:
   - Ask for totals, differences, or percentages
4. Memory behavior:
   - Ask follow-up questions that rely on prior turns
5. Tool logs:
   - Confirm tool usage JSON files are created in `logs/`

### Suggested Workflow Checks

- Intent routing reaches the expected node
- `tools_used` is populated when tools are invoked
- `actions_taken` accumulates correctly
- Conversation summary and active document IDs are updated
- State persists across turns for the same session/thread

## Built With

- LangChain
- LangGraph
- OpenAI Chat Models
- Pydantic
- Python dotenv

## License

See `../LICENSE.md` if present
