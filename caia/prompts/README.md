# CAIA Evaluation Framework Prompts

This directory contains all prompts used in the CAIA Ask Evaluator Framework. These prompts orchestrate the evaluation process, guiding models through question-answering tasks with and without tool access.

## Prompt Files

### 1. `reasoning_prompt_without_tool.md`

**Main Goal**: Generate direct answers with explicit reasoning when models have no tool access.

**Purpose**: Instructs models to answer questions using only their training knowledge and reasoning capabilities. The prompt requires both an answer and step-by-step reasoning in a structured JSON format, enabling evaluation of base model performance without external tool augmentation.

**Key Features**:
- Direct question-answering without tool access
- Structured JSON output with reasoning and answer fields
- Enables assessment of intrinsic model knowledge

---

### 2. `reasoning_prompt_with_tools.md`

**Main Goal**: Enable iterative tool selection and information gathering in an agentic workflow.

**Purpose**: Guides models through an iterative decision-making process where they analyze questions, strategically select tools, and decide when they have sufficient information. The prompt emphasizes tool selection over premature answer generation, aligning with agentic framework principles.

**Key Features**:
- Iterative tool selection (up to 5 iterations)
- Decision-making: continue tool calls or hand off to synthesis
- Structured JSON output with decision and reasoning
- Context-aware: considers previously gathered tool results

**Decision Flow**:
- If more information needed → call tools (`decision: "tool_call"`)
- If sufficient information gathered → hand off to synthesis (`decision: "synthesis"`)

---

### 3. `synthesis_prompt.md`

**Main Goal**: Synthesize gathered information into a comprehensive final answer.

**Purpose**: After tool execution completes, this prompt instructs the model to combine initial reasoning with all tool results into a coherent, complete answer. It ensures the final response incorporates all gathered information rather than fragmented tool outputs.

**Key Features**:
- Combines initial analysis with tool execution results
- Produces structured final answer with calculations and specific values
- Ensures comprehensive synthesis of all gathered information

---

### 4. `evaluation_judge_prompt.md`

**Main Goal**: Evaluate model responses against ground-truth answers using consistent scoring criteria.

**Purpose**: Instructs an LLM judge to compare model responses against expected outputs and assign binary scores (0.0 or 1.0). The prompt implements fair evaluation criteria that recognize partial correctness, semantic equivalence, and reasonable numerical tolerances.

**Key Features**:
- Binary scoring system (0.0 or 1.0)
- Fair evaluation: recognizes partial correctness and semantic equivalence
- Consistent criteria across all evaluations
- Detailed scoring rationale for transparency

## Evaluation Workflows

### Non-Tool Evaluation Flow
1. **Reasoning Prompt** → Model generates answer using only its knowledge
2. **Evaluation Judge** → Compares response to expected output and assigns score

### Tool-Enabled Evaluation Flow
1. **Reasoning Prompt (with tools)** → Model iteratively selects and calls tools
   - Model decides: continue tool calls or hand off to synthesis
   - Up to 5 iterations of tool selection and execution
2. **Synthesis Prompt** → Model synthesizes all gathered information into final answer
3. **Evaluation Judge** → Compares final answer to expected output and assigns score

## Key Design Principles

**Separation of Concerns**: Tool selection is separated from answer generation. The reasoning prompt focuses on information gathering, while synthesis produces the final answer.

**Agentic Decision-Making**: Models make informed decisions about tool usage based on what information they've gathered, enabling strategic rather than exhaustive tool execution.

**Structured Output**: All prompts use structured JSON formats to ensure parseable, consistent responses that facilitate automated evaluation and analysis.

## Related Documentation

For complete framework documentation, see:
- `caia/frameworks/` - Framework documentation and guides
- `caia/analysis/` - Analysis results and metrics
