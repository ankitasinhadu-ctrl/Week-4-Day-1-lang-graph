# NormalObjects LangGraph Lab - Jupyter Notebook Guide

## 📚 Overview

This comprehensive Jupyter notebook implements **Bloyce's Protocol** - a structured, rule-based complaint processing system using LangGraph.

**Key Feature**: Every step includes detailed explanations, expected outputs, and clear indicators for where human intervention is required.

---

## 🎯 Quick Navigation

| Step | Cell | What It Does | Human Input? |
|------|------|---|---|
| 1 | Installation | Installs required packages | ❌ No |
| 2 | API Setup | Configures OpenAI API key | ✋ Yes |
| 3 | Imports | Loads all libraries | ❌ No |
| 4 | State Definition | Defines ComplaintState TypedDict | ❌ No |
| 5 | LLM Init | Initializes ChatOpenAI | ❌ No |
| 6 | Intake Node | Creates categorization function | ❌ No |
| 7 | Validation Node | Creates rule-checking function | ❌ No |
| 8 | Investigation Node | Creates evidence-gathering function | ❌ No |
| 9 | Resolution Node | Creates solution-proposal function | ❌ No |
| 10 | Closure Node | Creates confirmation function | ✋ Yes |
| 11 | Build Graph | Connects all nodes with edges | ❌ No |
| 12 | Helper Functions | Utility functions for testing | ❌ No |
| 13 | Test Cases | Runs 6 test scenarios | ✋ Yes (×3 times) |
| 14 | Summary | Shows results | ❌ No |

---

## 📖 Detailed Step-by-Step Breakdown

### STEP 1: Installation
**Location**: First cell after title

**What It Does**:
- Installs 5 required packages: `langgraph`, `langchain`, `langchain-openai`, `python-dotenv`, `pydantic`
- Shows progress for each package
- Confirms successful installation

**Expected Output**:
```
Installing required packages...
==================================================
Installing langgraph...
✓ langgraph installed
Installing langchain...
✓ langchain installed
[... etc for all packages ...]
==================================================
All packages installed successfully!
```

**Human Input Required**: ❌ **NO**

**Troubleshooting**:
- If a package fails: Check your internet connection and try again
- If you see "PermissionError": Run `pip install --user` instead

---

### STEP 2: API Key Setup
**Location**: Second major section

**What It Does**:
1. Shows you where to get an OpenAI API key
2. Securely asks for your API key (input is hidden)
3. Validates and stores the key

**Expected Output**:
```
🔑 OpenAI API Key Setup
==================================================
You need an OpenAI API key to run this lab.
Get one free at: https://platform.openai.com/api-keys

Enter your OpenAI API key (it will be hidden): 

✓ API key set successfully!
  Key preview: sk-proj...xxx1234
```

**Human Input Required**: ✋ **YES**
- Go to https://platform.openai.com/api-keys
- Create a new API key (free tier available)
- Copy and paste it when prompted
- It will be hidden as you type

**Important Notes**:
- Don't share your API key with anyone
- It will be used for all LLM calls in this lab
- Free tier has usage limits, but sufficient for testing

---

### STEP 3: Imports
**Location**: After API setup

**What It Does**:
- Imports all necessary libraries from LangGraph, LangChain, and Python stdlib
- Shows what each import is used for
- Confirms all imports successful

**Expected Output**:
```
📚 Importing Libraries
==================================================
✓ TypedDict, StateGraph, END imported from LangGraph
✓ ChatOpenAI imported from LangChain
✓ HumanMessage, AIMessage imported
✓ datetime and json imported
==================================================

All imports successful!
```

**Human Input Required**: ❌ **NO**

---

### STEP 4: State Definition
**Location**: After imports

**What It Does**:
- Defines `ComplaintState` - a TypedDict that holds all workflow data
- Shows what each field is for
- Creates data structure that flows through all nodes

**State Structure**:
```
ComplaintState contains:
  INPUT DATA: complaint, category
  WORKFLOW TRACKING: status, workflow_path
  VALIDATION: is_valid, validation_details
  INVESTIGATION: investigation_notes, has_evidence
  RESOLUTION: resolution, effectiveness_rating
  CLOSURE: closure_confirmation, customer_satisfaction, closed_at, final_outcome
```

**Expected Output**:
```
📋 State Structure Defined
==================================================
ComplaintState contains:
  INPUT DATA:
    • complaint: The original complaint text
    • category: What type of complaint
  [... etc for all fields ...]
==================================================
```

**Human Input Required**: ❌ **NO**

**Key Concept**: State is **immutable** - each node creates new state instead of modifying existing

---

### STEP 5: LLM Initialization
**Location**: After state definition

**What It Does**:
- Creates ChatOpenAI instance using your API key
- Sets temperature to 0.3 (consistent, rule-following behavior)
- This LLM is used by all nodes

**Expected Output**:
```
🤖 LLM Initialized
==================================================
Model: gpt-4o-mini
Temperature: 0.3 (consistent, rule-following)
Status: Ready to use
==================================================
```

**Human Input Required**: ❌ **NO**

**Note**: Temperature 0.3 is chosen for consistency (0=deterministic, 1=creative)

---

### STEPS 6-10: Node Creation Functions
**Location**: Sections "Create INTAKE Node" through "Create CLOSURE Node"

**What They Do**:
Each step creates a function that processes state:
1. **INTAKE** (Step 6): Categorizes complaint into 5 categories
2. **VALIDATION** (Step 7): Checks against rule-based validation
3. **INVESTIGATION** (Step 8): Gathers evidence using LLM
4. **RESOLUTION** (Step 9): Proposes solution
5. **CLOSURE** (Step 10): Confirms application and customer satisfaction

**General Flow for Each Node**:
```python
def node_name(state: ComplaintState) -> ComplaintState:
    # 1. Extract relevant data from state
    # 2. Process using LLM
    # 3. Update state with results
    # 4. Return new state
```

**Expected Output (for each node)**:
```
✓ [node_name]_node function defined
```

**Human Input Required**: 
- Steps 6-9: ❌ **NO** (automatic)
- Step 10 (Closure): ✋ **YES** (see next section)

---

### STEP 10: Closure Node (IMPORTANT)
**Location**: "Create the CLOSURE Node" section

**What It Does**:
- Proposes closing the complaint
- **ASKS YOU** two questions:
  1. "Was the resolution successfully applied?" (yes/no)
  2. "What about customer satisfaction?" (satisfied/unsatisfied/pending)

**Expected Output**:
```
[STEP 5] CLOSURE NODE
==================================================

⚠️  HUMAN INTERVENTION REQUIRED ⚠️

Resolution to apply:
[shows the proposed resolution]

---------- QUESTION 1 ----------
Was the resolution successfully applied?
  Enter: yes / no
Your answer: yes          ← YOU TYPE HERE

---------- QUESTION 2 ----------
What about customer satisfaction?
  Enter: satisfied / unsatisfied / pending
Your answer: satisfied    ← YOU TYPE HERE

✓ Closure Processing Complete
  • Applied: True
  • Customer Satisfaction: satisfied
  • Closed at: 2024-01-15 14:23:45
```

**Human Input Required**: ✋ **YES** (×3 times during testing)

**What to Enter**:
- Question 1: Type `yes` or `no`
- Question 2: Type `satisfied`, `unsatisfied`, or `pending`

---

### STEP 11: Build the Graph
**Location**: "Build the Workflow Graph" section

**What It Does**:
- Creates StateGraph container
- Adds all 5 nodes
- Connects them with edges
- Creates conditional logic (validation branching)
- Compiles into executable graph

**Workflow Structure Visualized**:
```
START
  ↓
intake (categorize)
  ↓
validate (check rules)
  ├─→ VALID? → investigate → resolve → close → END
  └─→ INVALID? → END (REJECTED)
```

**Expected Output**:
```
BUILDING LANGGRAPH WORKFLOW
==================================================

✓ Adding nodes to graph...
  • intake_node added
  • validation_node added
  • investigation_node added
  • resolution_node added
  • closure_node added

✓ Setting entry point...
  • Entry point: intake

✓ Connecting nodes with edges...
  • intake → validate
  • validate → investigate (if valid)
  • validate → END (if invalid)
  • investigate → resolve
  • resolve → close
  • close → END

✓ Compiling workflow...
  • Workflow compiled successfully!

==================================================
WORKFLOW READY
==================================================
```

**Human Input Required**: ❌ **NO**

---

### STEP 12: Helper Functions
**Location**: "Create Helper Functions for Testing"

**What It Does**:
- `process_complaint()`: Runs a complaint through entire workflow
- `print_complaint_summary()`: Displays formatted results

**Expected Output**:
```
✓ Helper functions defined:
  • process_complaint(complaint_text) → runs workflow
  • print_complaint_summary(state) → displays results
```

**Human Input Required**: ❌ **NO**

---

### STEP 13: Testing Phase
**Location**: "Testing Phase" section with 6 test cells

**What It Does**:
Tests the workflow with different complaint types:

1. **Test 1 - PORTAL Complaint** (VALID)
   - Complaint about portal timing anomalies
   - Expected: Passes validation → Processes to closure
   - When you reach closure: Answer `yes` and `satisfied`

2. **Test 2 - MONSTER Complaint** (VALID)
   - Complaint about demogorgon behavior
   - Expected: Passes validation → Processes to closure
   - When you reach closure: Answer `yes` and `satisfied`

3. **Test 3 - PSYCHIC Complaint** (VALID)
   - Complaint about ability limitations
   - Expected: Passes validation → Processes to closure
   - When you reach closure: Answer `yes` and `satisfied`

4. **Test 4 - ENVIRONMENTAL Complaint** (VALID)
   - Complaint about power line anomalies
   - Expected: Passes validation → Processes to closure
   - When you reach closure: Answer `yes` and `satisfied`

5. **Test 5 - INVALID Complaint** (MISSING DETAILS)
   - Complaint with insufficient information
   - Expected: FAILS validation → REJECTED (no closure needed)

6. **Test 6 - OTHER Complaint** (MANUAL REVIEW)
   - Complaint that doesn't fit categories
   - Expected: Continues but marked for manual review
   - When you reach closure: Answer based on real-world judgment

**Expected Output for Valid Complaint**:
```
🧪 TEST 1: PORTAL COMPLAINT (VALID)
----------------------------------------------------------------------

[INTAKE] Processing complaint...
  🏷️ Category assigned: PORTAL

[VALIDATION NODE]
  🔍 Validating PORTAL complaint...
    Rule: Must reference specific location or timing anomalies
    LLM Response: YES
    Status: ✓ VALID

[INVESTIGATION NODE]
  🔬 Investigating PORTAL complaint...
  📋 Investigation Notes:
    • Temporal pattern identified...
    • Location consistency observed...
    • Environmental factors: [...]

[RESOLUTION NODE]
  💡 Developing resolution for PORTAL complaint...
  📢 Proposed Resolution:
    [Shows proposed fix]
    Effectiveness Rating: HIGH

[CLOSURE NODE]
  ⚠️  HUMAN INTERVENTION REQUIRED ⚠️
  
  QUESTION 1: Was the resolution successfully applied?
  Your answer: yes
  
  QUESTION 2: What about customer satisfaction?
  Your answer: satisfied

COMPLAINT PROCESSING SUMMARY
======================================================================
✓ WORKFLOW PATH: INTAKE → VALIDATE → INVESTIGATE → RESOLVE → CLOSE
✓ CATEGORY: PORTAL
✓ VALIDATION: VALID
✓ INVESTIGATION: Evidence gathered
✓ RESOLUTION: Applied
✅ CLOSURE: Confirmed
```

**Human Input Required**: ✋ **YES** (×3 during tests 1, 2, 3, 4, 6)
- Test 5 doesn't require human input (rejected automatically)

---

### STEP 14: Summary Report
**Location**: Last section

**What It Does**:
- Shows completion checklist
- Displays test results
- Confirms success criteria met
- Suggests optional extensions

**Expected Output**:
```
############################################################################
#                    LANGGRAPH LAB COMPLETION SUMMARY                     #
############################################################################

✅ COMPLETED STEPS:
   1. Setup and installation
   2. API key configuration
   [... etc ...]

📊 TEST RESULTS:
   • Test 1 (Portal): Processed successfully
   • Test 2 (Monster): Processed successfully
   [... etc ...]

🎯 SUCCESS CRITERIA MET:
   ✓ LangGraph state machine built
   ✓ Workflow follows all steps
   [... etc ...]
```

**Human Input Required**: ❌ **NO**

---

## 🔄 Complete Workflow Diagram

```
┌─────────────────────────────────────────────────────────┐
│                   COMPLAINT INPUT                        │
└────────────────────┬────────────────────────────────────┘
                     ↓
        ┌────────────────────────┐
        │   INTAKE NODE          │
        │ • Categorize complaint │
        │ • Add metadata         │
        └────────┬───────────────┘
                 ↓
        ┌────────────────────────┐
        │  VALIDATION NODE       │
        │ • Check rules          │
        │ • Category-specific    │
        └────────┬───────────────┘
                 ↓
           VALID? ──NO→ ✗ REJECT ──→ END
                 │
                YES
                 ↓
        ┌────────────────────────┐
        │ INVESTIGATION NODE     │
        │ • Gather evidence      │
        │ • LLM analysis         │
        └────────┬───────────────┘
                 ↓
        ┌────────────────────────┐
        │  RESOLUTION NODE       │
        │ • Propose solution     │
        │ • Rate effectiveness   │
        └────────┬───────────────┘
                 ↓
        ┌────────────────────────┐
        │   CLOSURE NODE         │
        │ ⚠️  ASK HUMAN:         │
        │ • Applied? (Y/N)       │
        │ • Satisfied? (3 opts)  │
        └────────┬───────────────┘
                 ↓
        ┌────────────────────────┐
        │  Final Outcome         │
        │ • Log results          │
        │ • Close complaint      │
        └────────┬───────────────┘
                 ↓
            ✅ END
```

---

## 📋 Data Flow Example

**Example: Portal Complaint**

```
INITIAL STATE:
{
  complaint: "Portal opens at different times...",
  category: "",
  status: "pending",
  ...
}

AFTER INTAKE:
{
  complaint: "Portal opens at different times...",
  category: "portal",  ← Added by intake_node
  status: "intake",
  workflow_path: ["intake"],
  ...
}

AFTER VALIDATION:
{
  ...(all above data)...
  is_valid: true,  ← Added by validation_node
  validation_details: "✓ Passes portal validation",
  status: "validate",
  workflow_path: ["intake", "validate"],
  ...
}

AFTER INVESTIGATION:
{
  ...(all above data)...
  investigation_notes: "• Temporal pattern...\n• Location consistency...",  ← Added
  has_evidence: true,
  status: "investigate",
  workflow_path: ["intake", "validate", "investigate"],
  ...
}

AFTER RESOLUTION:
{
  ...(all above data)...
  resolution: "Recommend standard portal monitoring procedure...",  ← Added
  effectiveness_rating: "high",
  status: "resolve",
  workflow_path: ["intake", "validate", "investigate", "resolve"],
  ...
}

AFTER CLOSURE:
{
  ...(all above data)...
  closure_confirmation: true,  ← Added from HUMAN INPUT
  customer_satisfaction: "satisfied",  ← Added from HUMAN INPUT
  closed_at: "2024-01-15 14:23:45",
  final_outcome: "Resolution applied: true | Customer satisfaction: satisfied | ...",
  status: "closed",
  workflow_path: ["intake", "validate", "investigate", "resolve", "close"],
  ...
}
```

---

## ⚠️ Where Human Intervention is Needed

### 1️⃣ STEP 2: API Key Entry
**What to do**: Enter your OpenAI API key (one-time setup)
**When**: Run first code cell in "API Key Setup" section
**How**: Paste your key when prompted (it won't be visible)

### 2️⃣ STEP 10: During Each Closure
**What to do**: Answer 2 questions about resolution outcome
**When**: During closure_node execution (happens 6 times in tests)
**How**: Type `yes`/`no` for question 1, then `satisfied`/`unsatisfied`/`pending` for question 2

**Total Human Interventions**: 1 (API key) + 6 (test closures) = **7 total**

---

## 🛠️ Troubleshooting

### "ModuleNotFoundError: No module named 'langgraph'"
**Solution**: Run the installation cell again. Make sure you have pip installed.

### "Authentication Error" when processing
**Solution**: Check your OpenAI API key is correct. Regenerate it if needed.

### LLM refuses to respond
**Solution**: Your API key might be exhausted. Get a new one or wait for quotas to reset.

### "Prompt too long" error
**Solution**: The complaint text is too long. Use shorter test cases.

### Node doesn't transition to next step
**Solution**: Check the edge connections in the graph. Make sure you ran the "Build Graph" cell.

---

## 📝 How to Modify for Your Own Complaints

To process your own complaint instead of test cases:

```python
# Instead of:
result_1 = process_complaint(portal_complaint)

# Use:
my_complaint = "Your custom complaint text here"
result = process_complaint(my_complaint)
print_complaint_summary(result)
```

The system will automatically:
1. Categorize it
2. Validate against rules
3. Investigate
4. Propose resolution
5. Ask for your confirmation

---

## 📚 Key Concepts Explained

### State Machine
A system that progresses through defined states (intake → validate → investigate → resolve → close). Unlike freeform agents, it MUST follow this path.

### TypedDict
A Python type that defines what fields a dictionary must contain and their types. Ensures data consistency.

### Edges
Connections between nodes that define workflow flow. Can be:
- **Simple**: A→B (always go this way)
- **Conditional**: A→B or A→C (choose based on condition)

### Immutable State
Each node doesn't modify state; it creates new state with additions. This makes debugging easier and enables undo/rollback.

### Audit Trail
The `workflow_path` list records all steps taken, providing complete traceability for compliance.

---

## ✅ Checklist: Before Submission

- [ ] Run all cells in order (don't skip any)
- [ ] Answer all human intervention prompts
- [ ] See "LANGGRAPH LAB COMPLETION SUMMARY" at end
- [ ] All 6 tests completed
- [ ] No error messages
- [ ] Save notebook as `.ipynb` file
- [ ] Create lab_summary.md with comparison paragraph
- [ ] Push to GitHub repository

---

## 🎓 Learning Outcomes

After completing this notebook, you will understand:

1. ✅ How to build structured workflows with LangGraph
2. ✅ How to design state machines for business logic
3. ✅ How to implement validation and branching logic
4. ✅ How to integrate LLM capabilities into structured flows
5. ✅ How LangGraph differs from LangChain agents
6. ✅ When to use each tool in real-world scenarios
7. ✅ How to create auditable, traceable AI systems

---

## 📞 Need Help?

1. **Check this guide** for the specific step
2. **Read cell output** - it usually explains what went wrong
3. **Review the comments** in code cells
4. **Restart kernel** if you run cells out of order
5. **Check OpenAI API status** if LLM fails

---

**Happy Labbing! 🚀**
