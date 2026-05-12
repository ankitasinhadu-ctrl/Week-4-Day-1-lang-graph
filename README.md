## LAB | NormalObjects - Strict Complaint Processor (LangGraph) Lab


README: How to Use This Lab
This repository contains a complete implementation of Bloyce's Protocol using LangGraph, a state machine framework for building structured AI workflows. The lab demonstrates how to build auditable, rule-based complaint processing systems that strictly follow defined steps: intake, validation, investigation, resolution, and closure. The NormalObjects_LangGraph_Lab_Notebook.ipynb file contains all executable code with 14 steps of implementation (setup through testing), while supporting guides ( HUMAN_INTERVENTION_GUIDE.md, NOTEBOOK_GUIDE.md) provide step-by-step explanations and troubleshooting. To run this lab: (1) Install dependencies using the first notebook cell, (2) Provide your OpenAI API key when prompted, (3) Run cells sequentially top-to-bottom, and (4) Answer human intervention prompts during the 6 test cases (you'll be asked "Was resolution applied?" and "Customer satisfaction level?" with simple yes/no/satisfied/unsatisfied/pending responses). The lab takes 40-90 minutes depending on whether you just execute code or read all explanations; see START_HERE.md for a 2-minute overview of learning paths, QUICK_CHEAT_SHEET.md for a 1-page cell-by-cell checklist, or NOTEBOOK_GUIDE.md for comprehensive deep-dive explanations of state management and workflow design.

Learning Outcomes
After completing this lab, you will understand:

How LangGraph state machines enforce structured workflows
Why immutable state and TypedDict schemas matter
How to design auditable AI systems with complete traceback
When to use LangGraph vs LangChain in production systems
How to integrate LLMs with rule-based logic for compliance
