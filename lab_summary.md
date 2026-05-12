# Lab Summary: NormalObjects LangGraph Lab 2

## LangGraph vs LangChain: A Structured Approach

**LangGraph excels at enforcing structured, rule-based workflows where every step must follow a predefined path and produce auditable results.** In this lab, the complaint processing system required intake → validate → investigate → resolve → close—a strict sequence that cannot be deviated from. LangGraph's state machine approach with explicit TypedDict definitions ensures that all nodes have access to consistent data and that state flows predictably through the system. By contrast, LangChain (Lab 1) takes a freeform agent approach where the AI decides which tools to call and in what order, making it flexible but harder to predict and audit. With LangGraph, validation failures immediately reject complaints and halt the workflow, investigations only proceed with evidence, and resolutions must reference established procedures—all enforced by the graph structure itself, not by agent judgment.

**The trade-off is clear: LangGraph sacrifices flexibility for control, making it ideal for compliance-heavy systems.** When you need to prove that every complaint followed the exact same process steps, that evidence was gathered before resolution, and that customer satisfaction was verified before closure, LangGraph's explicit state machine is superior. Each node's responsibility is singular and measurable (intake categorizes, validation checks rules, investigation gathers evidence), and the workflow path is recorded for audit purposes. LangChain's agent-based approach would require additional logging and would allow shortcuts or creative solutions that might violate Bloyce's Protocol. For financial systems, medical workflows, legal document processing, or any domain requiring regulatory compliance, LangGraph is the right choice. For creative problem-solving, exploratory chatbots, or customer service that benefits from unpredictable agent reasoning, LangChain remains superior.

---

## README: How to Use This Lab

This repository contains a complete implementation of Bloyce's Protocol using LangGraph, a state machine framework for building structured AI workflows. The lab demonstrates how to build auditable, rule-based complaint processing systems that strictly follow defined steps: intake, validation, investigation, resolution, and closure. The **NormalObjects_LangGraph_Lab_Notebook.ipynb** file contains all executable code with 14 steps of implementation (setup through testing), while supporting guides (QUICK_CHEAT_SHEET.md, HUMAN_INTERVENTION_GUIDE.md, NOTEBOOK_GUIDE.md) provide step-by-step explanations and troubleshooting. To run this lab: (1) Install dependencies using the first notebook cell, (2) Provide your OpenAI API key when prompted, (3) Run cells sequentially top-to-bottom, and (4) Answer human intervention prompts during the 6 test cases (you'll be asked "Was resolution applied?" and "Customer satisfaction level?" with simple yes/no/satisfied/unsatisfied/pending responses). The lab takes 40-90 minutes depending on whether you just execute code or read all explanations; see START_HERE.md for a 2-minute overview of learning paths, QUICK_CHEAT_SHEET.md for a 1-page cell-by-cell checklist, or NOTEBOOK_GUIDE.md for comprehensive deep-dive explanations of state management and workflow design.

## Learning Outcomes

After completing this lab, you will understand:
- How LangGraph state machines enforce structured workflows
- Why immutable state and TypedDict schemas matter
- How to design auditable AI systems with complete traceback
- When to use LangGraph vs LangChain in production systems
- How to integrate LLMs with rule-based logic for compliance
