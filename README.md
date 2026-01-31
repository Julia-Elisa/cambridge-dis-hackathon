# Kepler - Multi-Agent Fact Verification System

A sophisticated AI-powered fact-checking system that uses adversarial debate between specialized agents to verify claims against source truths. Instead of a single AI making black-box decisions, our system features a courtroom-style debate where agents argue, disagree, and negotiate to reach transparent, well-reasoned verdicts.

---

## 🎯 Project Overview

This system addresses the challenge: **"Is an external claim a faithful representation of an internal fact, or is it a mutation?"**

### The Multi-Agent Tribunal

Our system employs **4 specialized agents** in an adversarial debate architecture:

1. **Prosecutor** - Aggressively hunts for mutations, distortions, and misrepresentations
2. **Defense** - Argues for faithful interpretation and semantic equivalence
3. **Epistemologist** - Quantifies uncertainty and identifies ambiguous cases
4. **Jury Foreman** - Synthesizes arguments and delivers the final verdict

### Key Features

- **Adversarial Design**: Forces consideration of multiple perspectives
- **Transparent Reasoning**: Full debate transcripts show the decision-making process
- **Uncertainty Quantification**: Explicitly identifies ambiguous cases
- **Multi-Round Debates**: Agents can challenge and respond to each other's arguments
- **Mutation Detection**: Identifies 8 types of claim mutations (numerical distortion, missing context, causal confusion, etc.)

---

## 📋 Requirements

- **Python**: 3.11 or higher
- **OpenAI API Key**: Required for running the agents

---

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone <repository-url>
cd cambridge-dis-hackathon
```

### 2. Set Up Environment

#### Option A: Using Conda (Recommended)

```bash
# Create environment from environment.yml
conda env create -f environment.yml

# Activate environment
conda activate hackathon
```

### 3. Set Up API Key

```bash
# Set your OpenAI API key as an environment variable
export OPENAI_API_KEY='your-api-key-here'
```

Or create a `.env` file in the project root:

```
OPENAI_API_KEY=your-api-key-here
```

### 4. Run the System

Navigate to the `kepler` directory:

```bash
cd kepler
```

#### Basic Usage (Strategic Cases)

Run with pre-selected strategic cases that showcase different mutation types:

```bash
python main.py
```

This will analyze 5 carefully selected cases demonstrating:
- Numerical boundary manipulation
- Added information
- Negation framing
- Borderline rounding
- Faithful representation

#### Other Usage Options

```bash
# Run specific cases by index
python main.py --cases 0,1,2

# Interactive case selection
python main.py --interactive

# Run all cases (expensive!)
python main.py --all

# Presentation mode (uses gpt-4.1 instead of gpt-4.1-mini)
python main.py --presentation
```

---

## 📊 System Comparison

Compare the multi-agent system against a single-agent baseline:

```bash
cd kepler
python compare_systems.py
```

This will:
- Run both single-agent and multi-agent systems on the same cases
- Generate a detailed comparison report (`comparison_report.md`)
- Export results to JSON files for further analysis
- Show verdict agreements/disagreements and confidence differences

---

## 📁 Project Structure

```
cambridge-dis-hackathon/
├── kepler/                          # Main source code
│   ├── agents.py                    # Multi-agent debate system
│   ├── main.py                      # Primary entry point
│   ├── compare_systems.py           # Single vs multi-agent comparison
│   ├── single_agent_baseline.py     # Simple baseline for comparison
│   ├── visualize.py                 # Visualization and export utilities
│   ├── demo.py                      # Demo script
│   ├── export_comparison_data.py    # Data export utilities
│   ├── export_debates.py            # Debate transcript export
│   ├── view_raw_responses.py        # View raw agent responses
│   ├── Kepler.csv                   # Dataset (claim-truth pairs)
│   └── requirements.txt             # Python dependencies
├── requirements.txt                 # Root dependencies
├── environment.yml                  # Conda environment specification
├── README.md                        # This file
├── Instructions.md                  # Hackathon instructions
├── LICENSE                          # License file
└── *.json                           # Output files (results, debates, etc.)
```

---

## 🔍 Understanding the Output

### Verdict Types

- **FAITHFUL**: The external claim accurately represents the internal fact
- **MUTATED**: The claim distorts, exaggerates, or misrepresents the fact
- **AMBIGUOUS**: Genuine uncertainty exists; reasonable interpretations differ

### Mutation Types Detected

1. **Numerical Distortion**: Changed numbers or statistical boundaries
2. **Missing Context**: Omitted crucial contextual information
3. **Causal Confusion**: Misrepresented cause-effect relationships
4. **Exaggeration**: Amplified or dramatized claims
5. **Scope Change**: Altered the scope or generality of the claim
6. **Temporal Mismatch**: Changed time references or periods
7. **Added Information**: Introduced details not in the source
8. **Negation Framing**: Reframed using negation (e.g., "failed to" vs "did not")

### Sample Output

```
FINAL VERDICT: AMBIGUOUS (80% confidence)

REASONING: The external claim closely approximates the original death toll 
figure with minor inequality inversion and omission of additional 
epidemiological data...

PROSECUTOR ARGUMENTS:
- Inverts inequality direction from lower bound to upper bound
- Removes broader epidemiological context

DEFENSE ARGUMENTS:
- Uses close numerical figure within narrow range
- Focusing on death toll is common journalistic practice

EPISTEMOLOGIST ANALYSIS:
- Core uncertainty: Whether inequality inversion constitutes meaningful 
  distortion or acceptable paraphrasing
```

---

## 📈 Output Files

Running the system generates several output files:

- `debate_results.json` - Full debate results with all agent responses
- `multi_agent_results.json` - Multi-agent system results
- `single_agent_results.json` - Single-agent baseline results
- `comparison_report.md` - Detailed comparison analysis
- `comparison_dashboard.html` - Interactive visualization (if generated)
- `visualization_data_*.json` - Data for visualizations

### Why Multi-Agent Beats Single-Agent

1. **Adversarial Testing**: Prosecutor and Defense challenge each other
2. **Bias Reduction**: Multiple perspectives prevent single-viewpoint bias
3. **Calibrated Confidence**: Debate leads to more realistic confidence scores
4. **Transparent Process**: Full debate transcript enables human oversight
5. **Nuanced Analysis**: Multi-round exchanges capture subtle distinctions

---

## 🛠️ Development Tips

### Cost Management

- **Development**: Use `gpt-4.1-mini` (default) for testing
- **Presentation**: Use `--presentation` flag for `gpt-4.1` only during demos

### Debugging

```bash
# View raw agent responses
python view_raw_responses.py

# Export debate transcripts
python export_debates.py
```
