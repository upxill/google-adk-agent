# google-adk-agent

A small Google ADK agent workspace with example agents and tools.

## Quick Overview

- Purpose: Example agents demonstrating use of the Google ADK `Agent` and `FunctionTool` patterns.
- Location: each agent lives in its own folder (for example `get_current_time`).

## Requirements

- macOS / Linux
- Python 3.13
- A working virtual environment (recommended: `.venv`)
- `adk` CLI (Google ADK) available on PATH if you plan to run `adk web` or other ADK commands

## Setup

1. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
```

2. Install dependencies (if you have a `requirements.txt` or otherwise).

3. Create a `.env` file in the agent folder or workspace root and set required environment variables. Example:

```dotenv
# .env
GOOGLE_API_KEY=your_api_key_here
GOOGLE_GENAI_USE_VERTEXAI=0
```

Do not commit secrets to version control.

## Running the agent (development)

Start the ADK web server for local debugging:

```bash
adk web
```

If you created an agent using the ADK CLI (for example `adk create get_current_time`), the generated agent folder will contain an `agent.py` exposing an `Agent` instance called `root_agent`.

## Agent structure

- `agent.py` — defines an `Agent` (from `google.adk.agents.llm_agent`) and registers tools.
- Tools that wrap Python functions should use `FunctionTool` from `google.adk.tools`:

```python
from google.adk.tools import FunctionTool

def get_current_time(city: str) -> dict:
    return {'status': 'success', 'city': city, 'time': '10:30 AM'}

root_agent = Agent(..., tools=[
    FunctionTool(function=get_current_time, description='Get current time', parameters={'city': {'type': 'string'}})
])
```

## Notes


- Keep secrets out of the repo. Use `.env` and OS-level secret managers for production keys.

## Troubleshooting

- Validation errors when loading agents usually indicate invalid `tools` entries: ensure each tool is an instance of the ADK `Tool` classes (e.g., `FunctionTool`) rather than plain dictionaries or callables.

## Contributing

Open a pull request with changes to agents or tooling. Keep changes small and include a brief description of what the agent does.

## License

MIT-style — adapt as needed.
# google-adk-agent
Google ADK
