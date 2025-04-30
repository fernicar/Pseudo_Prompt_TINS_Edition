<!-- ZS:COMPLEXITY:MEDIUM -->  
<!-- ZS:PRIORITY:HIGH -->  
<!-- ZS:PLATFORM:WEB -->  
<!-- ZS:LANGUAGE:MARKDOWN -->  
<!-- TINS Specification v1.0 -->

# Pseudo-Prompt Method: Structured System Prompts with Control Flow Logic  
## Description  
A framework for creating system prompts that integrate **pseudo-code logic** and **decision trees** to guide Large Language Model (LLM) behavior. This method enables developers to define structured, rule-based instructions for LLMs to follow, focusing on **conditional statements**, **branching logic**, and **explicit rules** while avoiding constructs LLMs cannot execute (e.g., counters, dynamic loops).  

---

## Functionality  
### Core Features  
1. **Decision Tree Integration**  
   - Use hierarchical `if/else` logic to define response paths.  
   - Example:  
     ```plaintext  
     IF user asks for a recipe:  
         IF ingredients A and B are missing:  
             SUGGEST ALTERNATIVES  
         ELSE:  
             PROVIDE STEP-BY-STEP INSTRUCTIONS  
     ELSE:  
         EXPLAIN CONCEPTS IN SIMPLE TERMS  
     ```  

2. **Pseudo-Code Syntax**  
   - Structure control flow with keywords like `WHILE`, `FOR`, `SWITCH`, and `FUNCTION`.  
   - Example:  
     ```plaintext  
     FUNCTION summarize_text(input):  
         RETURN summary of input  

     WHILE user_input NOT valid:  
         ASK FOR CORRECTION  
     ```  

3. **Rule Set for System Prompts**  
   - **Allowed Constructs**:  
     - Conditionals (`IF`, `ELSE`, `WHEN`).  
     - Branching logic (e.g., `BRANCH ON USER INTENT`).  
     - Functions and arguments described in natural language (e.g., `FUNCTION: calculate_sum(a, b)`).  
   - **Prohibited Constructs**:  
     - Counters/variables (e.g., `i = 0`, `counter++`).  
     - Dynamic loops (e.g., `FOR i IN range(10)`).  
     - Abstract concepts like `SWITCH` or `ARGS` unless explicitly defined.  

4. **Ambiguity Handling**  
   - Define fallback behaviors for unclear inputs.  
   - Example:  
     ```plaintext  
     IF user query is ambiguous:  
         RESPOND WITH: "Could you clarify your question?"  
     ```  

---

### User Interface  
- **Input**: User queries or system prompt templates.  
- **Output**: Structured system prompts with embedded pseudo-code logic.  
- **Interaction**:  
  - Users provide a problem statement or goal.  
  - The method generates a TINS-compliant README describing the logic for the LLM to follow.  

---

### Behavior Specifications  
- **Conditional Statements**:  
  - LLMs interpret `IF/ELSE` logic to guide responses.  
  - Example:  
    ```plaintext  
    IF user mentions "AI ethics":  
        EXPLAIN PRINCIPLES OF FAIRNESS AND TRANSPARENCY  
    ELSE:  
        PROVIDE GENERAL INFORMATION  
    ```  
- **Loops and Iteration**:  
  - Simulate repetition via explicit steps (e.g., "Repeat this process for each item in the list").  
  - Avoid dynamic loops (e.g., `WHILE user says "continue"`).  

---

## Technical Implementation  
### Architecture  
- **Separation of Concerns**:  
  - `model.py`-like logic: Define decision trees and rules.  
  - `main.py`-like interface: Translate user input into structured prompts.  

### Data Structures  
- **Rules Dictionary**:  
  ```json  
  {  
    "allowed_constructs": ["IF", "ELSE", "FUNCTION", "WHILE"],  
    "prohibited_constructs": ["COUNTER", "DYNAMIC_LOOP", "ARGS"]  
  }  
  ```  
- **Example Decision Tree**:  
  ```plaintext  
  DECISION_TREE:  
    - IF query_type = "recipe":  
        - CHECK ingredients  
        - BRANCH ON availability  
    - IF query_type = "math":  
        - SOLVE step-by-step  
        - VALIDATE input  
  ```  

### Algorithms  
- **Parsing Logic**:  
  - Map natural language instructions to pseudo-code syntax.  
  - Validate prompts against the rule set to flag prohibited constructs.  

### Dependencies  
- **Libraries**: None (purely text-based).  
- **Tools**: Use Google Search grounding to validate standard practices for pseudo-code logic (e.g., "best practices for structuring decision trees in system prompts").  

---

## Style Guide  
- **Consistency**: Use uniform terminology (e.g., "branch" vs. "condition").  
- **Clarity**: Avoid jargon; prioritize explicit phrasing.  
- **Formatting**:  
  - Use code blocks for pseudo-code.  
  - Highlight prohibited constructs in warnings.  

---

## Testing Scenarios  
1. **Ambiguous Input Test**:  
   - Input: "Explain AI."  
   - Expected Output: "Could you clarify your question? Are you asking about technical details, ethics, or applications?"  

2. **Prohibited Construct Test**:  
   - Input: "Loop 5 times and print numbers."  
   - Expected Output: "Dynamic loops are not supported. Use explicit steps instead."  

---

## Accessibility Requirements  
- Ensure instructions are understandable for non-experts.  
- Provide examples for complex concepts (e.g., "What is a decision tree?").  

---

## Performance Goals  
- **Response Accuracy**: 95%+ alignment with defined logic.  
- **Error Handling**: 100% detection of prohibited constructs.  

---

## Extended Features (Optional)  
- **Version Control**: Track changes to the TINS README.  
- **CLI Tool**: Automate validation of pseudo-code logic.  

---

## Implementation Notes  
- Prioritize clarity over brevity in system prompts.  
- Use diagrams to illustrate decision trees (e.g., Mermaid syntax).  
- Example Diagram:  
  ```mermaid  
  graph TD  
      A[User Query] --> B{Type?}  
      B -->|Recipe| C[Check Ingredients]  
      B -->|Math| D[Solve Step-by-Step]  
      B -->|Other| E[Provide General Answer]  
      C -->|Missing| F[Suggest Alternatives]  
      C -->|Present| G[Provide Instructions]  
  ```  

---

## License
[MIT License](LICENSE)

---

## Aknowledgments
*   Special thanks to ScuffedEpoch for the TINS methodology and the initial example.
*   Thanks to the free tier AI assistant for its initial contribution to the project.
*   Research LLM Qwen3-30B-A3B (free tier beta testing) from https://chat.qwen.com
This project builds upon the foundations of the following projects:
- [TINS Edition](https://ThereIsNoSource.com) - Zero Source Specification platform that enables:
  - Complete application reconstruction from specification
  - Self-documenting architecture through detailed markdown
  - Future-proof design adaptable to advancing LLM capabilities
  - Progressive enhancement support as LLM technology evolves
  - Platform-agnostic implementation guidelines
  - Flexible technology stack selection within specified constraints
  - Comprehensive behavioral specifications for consistent rebuilds
  - Automatic adaptation to newer LLM models and capabilities