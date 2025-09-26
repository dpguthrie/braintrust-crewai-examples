# Braintrust CrewAI Examples - Repository Structure

This document provides a comprehensive folder and file tree for the `braintrust-crewai-examples` repository.

## Repository Overview

This repository contains a CrewAI example project focused on lead scoring and email generation workflows. The project uses the Braintrust platform for tracing and evaluation of AI agent performance.

## Directory Structure

### Complete Tree View

```
braintrust-crewai-examples/
├── .env.example                              # Environment variables template
├── .git/                                     # Git repository metadata
├── .gitignore                                # Git ignore rules
├── README.md                                 # Project documentation
├── pyproject.toml                            # Python project configuration
├── uv.lock                                   # UV package manager lock file
└── src/                                      # Source code directory
    └── lead_score/                           # Main application package
        ├── __init__.py                       # Package initialization
        ├── constants.py                      # Application constants (job descriptions, skills)
        ├── flow_types.py                     # Pydantic models for data structures
        ├── leads.csv                         # Sample lead data for processing
        ├── main.py                           # Main application entry point and flow logic
        ├── tracing.py                        # Braintrust tracing configuration
        ├── crews/                            # CrewAI crew definitions
        │   ├── lead_response_crew/           # Crew for generating email responses
        │   │   ├── config/                   # Configuration files for lead response crew
        │   │   │   ├── agents.yaml           # Agent definitions and configurations
        │   │   │   └── tasks.yaml            # Task definitions for email generation
        │   │   └── lead_response_crew.py     # Lead response crew implementation
        │   └── lead_score_crew/              # Crew for scoring leads
        │       ├── config/                   # Configuration files for lead scoring crew
        │       │   ├── agents.yaml           # Agent definitions and configurations
        │       │   └── tasks.yaml            # Task definitions for lead evaluation
        │       └── lead_score_crew.py        # Lead scoring crew implementation
        ├── tools/                            # Custom tools for agents
        │   ├── __init__.py                   # Tools package initialization
        │   └── custom_tool.py                # Custom tool implementations
        └── utils/                            # Utility functions
            └── candidateUtils.py             # Utilities for candidate data processing
```

### Simplified Tree View

```
braintrust-crewai-examples/
├── README.md
├── pyproject.toml
├── .env.example
└── src/lead_score/
    ├── main.py                               # Main flow logic
    ├── constants.py                          # Job descriptions & skills
    ├── flow_types.py                         # Data models
    ├── leads.csv                             # Sample data
    ├── tracing.py                            # Braintrust setup
    ├── crews/
    │   ├── lead_score_crew/                  # Candidate evaluation
    │   └── lead_response_crew/               # Email generation
    ├── tools/custom_tool.py                  # Agent tools
    └── utils/candidateUtils.py               # Data utilities
```

## File Descriptions

### Root Level Files

- **`.env.example`**: Template file showing required environment variables (e.g., `OPENAI_API_KEY`)
- **`.gitignore`**: Specifies files and directories to be ignored by Git version control
- **`README.md`**: Main project documentation with installation and usage instructions
- **`pyproject.toml`**: Python project configuration file defining dependencies and build settings
- **`uv.lock`**: Lock file for the UV package manager ensuring reproducible builds

### Source Code (`src/lead_score/`)

#### Core Application Files

- **`__init__.py`**: Makes the directory a Python package
- **`constants.py`**: Contains job descriptions, required skills, and other application constants
- **`flow_types.py`**: Defines Pydantic models for data structures:
  - `JobDescription`: Job posting details
  - `Candidate`: Lead candidate information
  - `CandidateScore`: Scoring results
  - `ScoredCandidate`: Combined candidate and score data
- **`leads.csv`**: Sample CSV file containing lead data for processing
- **`main.py`**: Main application file containing:
  - `LeadScoreState`: Application state management
  - `LeadScoreFlow`: Core workflow logic with async operations
  - Flow methods for loading leads, scoring, and generating emails
- **`tracing.py`**: Braintrust tracing setup for monitoring and evaluation

#### Crews Directory (`crews/`)

Contains two main crew implementations:

##### Lead Score Crew (`lead_score_crew/`)
- **`lead_score_crew.py`**: Implements the crew responsible for evaluating and scoring candidates
- **`config/agents.yaml`**: Defines the HR evaluation agent configuration
- **`config/tasks.yaml`**: Defines the candidate evaluation task

##### Lead Response Crew (`lead_response_crew/`)
- **`lead_response_crew.py`**: Implements the crew responsible for generating personalized email responses
- **`config/agents.yaml`**: Defines the email follow-up agent configuration
- **`config/tasks.yaml`**: Defines the email generation task

#### Tools Directory (`tools/`)
- **`__init__.py`**: Package initialization
- **`custom_tool.py`**: Custom tool implementations for use by agents

#### Utils Directory (`utils/`)
- **`candidateUtils.py`**: Utility functions for processing and combining candidate data

## Workflow Overview

The application implements a lead scoring and email generation workflow:

1. **Load Leads**: Reads candidate data from `leads.csv`
2. **Score Leads**: Uses the Lead Score Crew to evaluate candidates against job requirements
3. **Human Review**: Provides option for human feedback on scoring
4. **Generate Emails**: Creates personalized email responses using the Lead Response Crew
5. **Output**: Saves generated emails to individual text files

## Key Technologies

- **CrewAI**: Multi-agent AI framework for orchestrating AI agents
- **Braintrust**: Platform for tracing and evaluating AI agent performance
- **Pydantic**: Data validation and settings management
- **OpenTelemetry**: Observability and tracing
- **UV**: Modern Python package manager
- **Python 3.10+**: Core programming language

## Configuration Files

The project uses YAML configuration files to define:
- **Agents**: AI agents with specific roles, goals, and capabilities
- **Tasks**: Specific tasks that agents need to complete
- **Environment**: Required API keys and settings through `.env` file

## Runtime Generated Directories

During execution, the application may create additional directories:

- **`src/lead_score/email_responses/`**: Created at runtime to store generated email files
  - Contains individual `.txt` files for each candidate's personalized email
  - File names are sanitized versions of candidate names (e.g., `John_Smith.txt`)

## Usage

To run the application:
```bash
crewai run
```

This will execute the lead scoring flow and generate personalized emails in the `email_responses` directory.

---

This structure provides a clean separation of concerns and makes the application highly configurable and maintainable.