# Mathematical Proof Analysis for Code Module

Analyze a code module as a mathematician/logician to create a formal finite state machine representation and identify edge cases, invariant violations, and logical inconsistencies.

**Module/File Path:** $ARGUMENTS

## Steps:

1. **Parse Module Structure**
   - Read the specified file/module
   - Identify all functions, classes, and their relationships
   - Extract type definitions, interfaces, and contracts
   - Map input/output relationships

2. **Build Formal Model**
   - Create finite state machine representation:
     - **States**: All possible states the module can be in
     - **Transitions**: Function calls and state changes
     - **Inputs**: Parameters, external dependencies
     - **Outputs**: Return values, side effects
   - Define invariants that should always hold
   - Identify preconditions and postconditions

3. **Formal Analysis**
   - **State Space Analysis**:
     - Enumerate all reachable states
     - Identify unreachable code paths
     - Find absorbing states (no exit)
   - **Transition Analysis**:
     - Verify all transitions are well-defined
     - Check for non-deterministic behavior
     - Identify race conditions
   - **Invariant Checking**:
     - List all invariants that should hold
     - Prove or disprove each invariant
     - Find states where invariants break

4. **Edge Case Discovery**
   - **Boundary Analysis**:
     - Numeric overflows/underflows
     - Empty collections/null values
     - Maximum/minimum values
   - **State Explosion**:
     - Combinatorial state growth
     - Recursive depth issues
   - **Concurrency Issues**:
     - Race conditions
     - Deadlock scenarios
     - Atomicity violations
   - **Type Safety**:
     - Implicit conversions
     - Type coercion edge cases
     - Generic type constraints

5. **Proof Construction**
   - For each critical function:
     - State the theorem (what it should do)
     - List assumptions/preconditions
     - Provide proof sketch or counterexample
     - Identify where proofs fail
   - Use formal notation where helpful:
     ```
     ∀ x ∈ Input : Precondition(x) ⟹ Postcondition(f(x))
     ```

6. **Generate Excalidraw Diagram**
   - Create visual FSM representation in Excalidraw format
   - Include states, transitions, and annotations
   - Save to Obsidian vault with proper linking
   - Generate both `.excalidraw` file and embedded markdown

7. **Generate Report in Obsidian Vault**
   - Create analysis document in: `${OBSIDIAN_VAULT}/claude-sessions/${PARENT_DIR}/${PROJECT_NAME}/`
   - Filename: `proof-${MODULE_NAME}-${DATE}.md`
   - Content structure:
   ```markdown
   # Formal Analysis of [Module Name]
   
   ## Finite State Machine Model
   ![[module-name-fsm.excalidraw]]
   
   ## State Transition Table
   | Current State | Input/Event | Next State | Conditions |
   |--------------|-------------|------------|------------|
   | INIT | parse() | PARSING | valid input |
   | PARSING | error | ERROR | invalid syntax |
   
   ## Invariants
   ✓ Invariant 1: [Description] - HOLDS
   ✗ Invariant 2: [Description] - VIOLATED in state X
   
   ## Edge Cases Discovered
   1. **[Edge Case Name]**
      - Condition: [When it occurs]
      - Impact: [What breaks]
      - Proof: [Mathematical reasoning]
      - Visual: ![[edge-case-1.excalidraw]]
   
   ## Formal Proofs
   ### Theorem 1: [Function correctness]
   - Hypothesis: [Preconditions]
   - Conclusion: [Postconditions]
   - Proof: [Sketch or counterexample]
   
   ## Recommendations
   - Add guards for [edge case]
   - Strengthen invariant [X]
   - Consider [architectural change]
   ```

## Example Usage:
```
Command: atm-proof src/utils/parser.ts

Output:
Analyzing module: src/utils/parser.ts
Creating formal analysis in Obsidian vault...

Generated files:
- Analysis report: ~/Documents/Obsidian/Development/claude-sessions/project-name/proof-parser-2024-01-15.md
- FSM diagram: ~/Documents/Obsidian/Development/claude-sessions/diagrams/project-name/parser-fsm-2024-01-15.excalidraw
- Edge case diagrams: ~/Documents/Obsidian/Development/claude-sessions/diagrams/project-name/edge-case-*.excalidraw

## Finite State Machine Model
States: {INIT, PARSING, ERROR, COMPLETE}
Transitions:
  INIT → PARSING (on: parse())
  PARSING → ERROR (on: invalid input)
  PARSING → COMPLETE (on: valid parse)
  ERROR → INIT (on: reset())

## Edge Cases Discovered
1. **Stack Overflow on Nested Input**
   - Condition: Input with depth > 1000
   - Proof: No recursion limit check
   - Fix: Add depth parameter with limit

2. **Integer Overflow in Buffer Size**
   - Condition: size * count > MAX_INT
   - Proof: size × count ∈ ℤ but implementation assumes ∈ ℕ
   - Fix: Add overflow check before allocation
```

## Analysis Techniques:

### Abstract Interpretation
- Approximate program behavior
- Track value ranges and constraints
- Identify impossible states

### Hoare Logic
- {P} S {Q} - If P before S, then Q after S
- Build proof obligations
- Verify with SMT solver reasoning

### Model Checking
- Enumerate state space
- Check temporal properties
- Find counterexamples

## Focus Areas:
- Memory safety (buffer overflows, use-after-free)
- Numeric safety (overflow, division by zero)
- Concurrency safety (data races, deadlocks)
- Logic errors (off-by-one, incorrect conditionals)
- API contracts (precondition violations)

## Notes:
- Uses mathematical notation where it adds clarity
- Focuses on provable properties and counterexamples
- Provides actionable fixes for discovered issues
- Think like a mathematician: "What can go wrong?"

## Excalidraw Integration:

### File Generation
When generating Excalidraw diagrams:

1. **Create `.excalidraw` files** in the Obsidian vault:
   - Path: `{OBSIDIAN_VAULT}/claude-sessions/diagrams/{project-name}/`
   - Naming: `{module-name}-fsm-{date}.excalidraw`

2. **Excalidraw JSON Format**:
   ```json
   {
     "type": "excalidraw",
     "version": 2,
     "elements": [
       {
         "type": "ellipse",
         "id": "state-init",
         "x": 100,
         "y": 100,
         "width": 120,
         "height": 60,
         "strokeColor": "#000000",
         "backgroundColor": "#ffffff",
         "fillStyle": "solid",
         "text": "INIT"
       },
       {
         "type": "arrow",
         "id": "transition-1",
         "x": 220,
         "y": 130,
         "width": 100,
         "height": 0,
         "strokeColor": "#000000",
         "startBinding": {"elementId": "state-init"},
         "endBinding": {"elementId": "state-parsing"},
         "text": "parse()"
       }
     ]
   }
   ```

3. **Diagram Elements**:
   - **States**: Ellipses or rectangles with state names
   - **Transitions**: Arrows with labels for triggers/conditions
   - **Annotations**: Text elements for invariants and notes
   - **Groups**: Dotted rectangles for subsystems
   - **Colors**:
     - Green: Safe states
     - Yellow: Warning states
     - Red: Error states
     - Blue: External interfaces

4. **Link in Obsidian**:
   ```markdown
   ![[parser-fsm-2024-01-15.excalidraw|800]]
   ```

### Example FSM Diagram Structure:
- Initial state (double circle)
- Normal states (circles)
- Error states (red circles)
- Final states (double circle with dot)
- Transitions with guards [condition]
- Actions on transitions /action
- Self-loops for repeated operations

### Auto-save to Obsidian:
The diagram files should be automatically saved to the same Obsidian vault structure used for session logging, making them accessible and linked from the analysis reports.

### Implementation Note:
When running atm-proof, Claude will:
1. Analyze the code module mathematically
2. Get project information from git context
3. Create Obsidian vault directory structure if needed:
   ```bash
   OBSIDIAN_VAULT="${OBSIDIAN_VAULT:-$HOME/Documents/Obsidian/Development}"
   PROJECT_NAME=$(basename $(git rev-parse --show-toplevel 2>/dev/null) || echo "unknown")
   PARENT_DIR=$(basename $(dirname $(git rev-parse --show-toplevel 2>/dev/null)) || echo "projects")
   
   REPORT_DIR="${OBSIDIAN_VAULT}/claude-sessions/${PARENT_DIR}/${PROJECT_NAME}"
   DIAGRAM_DIR="${OBSIDIAN_VAULT}/claude-sessions/diagrams/${PROJECT_NAME}"
   
   mkdir -p "$REPORT_DIR" "$DIAGRAM_DIR"
   ```
4. Generate Excalidraw diagrams using the helper script:
   ```bash
   ~/.claude/hooks/excalidraw-generator.sh fsm "module-name" "project-name" "STATE1,STATE2,STATE3" "transitions"
   ```
5. Save the analysis report as markdown in Obsidian:
   ```bash
   REPORT_FILE="${REPORT_DIR}/proof-${MODULE_NAME}-$(date +%Y-%m-%d-%H%M).md"
   echo "$ANALYSIS_CONTENT" > "$REPORT_FILE"
   ```
6. Link diagrams in the report using: `![[diagram-name.excalidraw]]`

The analysis will be immediately available in your Obsidian vault with all diagrams properly linked and viewable.