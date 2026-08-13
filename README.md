# SmartHomeIoTNLU Dataset

**SmartHomeIoTNLU: A Context-Rich Smart Home Dataset for Natural Language Understanding and Coordinated Multi-Device IoT Control**

SmartHomeIoTNLU is a synthetic, context-rich dataset designed to support research in **Natural Language Understanding (NLU)**, **context-aware reasoning**, and **single-device and coordinated multi-device IoT control** in smart home environments.

The dataset provides structured mappings between:

- Natural language user commands
- User intent
- Smart home environmental context
- IoT device states
- Single-device actions
- Coordinated multi-device actions
- Device-specific parameters

SmartHomeIoTNLU enables the development and evaluation of intelligent IoT systems that require understanding user commands, reasoning about environmental context, and generating executable device actions.

---

# Dataset Applications

SmartHomeIoTNLU supports research and development in the following areas:

## Natural Language Understanding

- Intent classification
- Semantic command understanding
- Natural language grounding
- Command-to-action mapping
- Smart home conversational assistants

## Smart Home Intelligence

- Single-device action prediction
- Multi-device action prediction
- Context-aware smart home automation
- Intelligent IoT control systems
- Smart home assistants

## Artificial Intelligence and Machine Learning

- Machine learning benchmarking
- Large Language Model (LLM) fine-tuning
- Retrieval-Augmented Generation (RAG)
- Intelligent IoT agents
- AI agent planning
- Context-aware computing
- Continual learning

## Human-Centered AI

- Human–AI interaction
- Intelligent home automation
- Context-aware decision making
- Adaptive smart environments

---

# Dataset Overview

SmartHomeIoTNLU represents interactions between users and a simulated smart home environment.

Each interaction contains:

1. A natural language user command
2. Environmental context
3. Device state information
4. Executable device action representation

The output representation contains:

- Target device(s)
- Device actions
- Optional device-specific parameters

---

# Example Interaction

## User Command
Prepare my bedroom for sleeping

## Context
Location: Bedroom
Time: Night
Temperature: 25°C
Occupancy: 1
Light: 20%
Noise: Low


## Generated Actions

| Device | Action |
|---|---|
| Light | OFF |
| Curtains | CLOSE |
| AC | ADJUST (22°C) |
| TV | OFF |
| Bed Lamp | ON |
| Noise Machine | ON |
| Air Purifier | ON |

A single user command can therefore produce coordinated actions across multiple IoT devices.

---

# Smart Home Environment

SmartHomeIoTNLU models a residential smart home environment consisting of:

- 5 room types
- 19 IoT device categories
- Multiple environmental conditions
- Single-device and multi-device automation scenarios

Supported rooms:

- Bedroom
- Living Room
- Kitchen
- Study Room
- Dining Room

Environmental context includes:

- Temperature
- Light level
- Noise level
- Occupancy
- Time period
- Location

---

# Dataset Statistics

| Property | Value |
|---|---:|
| Total Event IDs | 200,320 |
| Total Rows | 743,960 |
| Unique Commands | 2,037 |
| Intent Types | 2 |
| Scenarios | 23 |
| Rooms | 5 |
| Device Types | 19 |
| Action Types | 5 |
| Parameter Values | 25 |
| Vocabulary Size | 533 |
| Average Actions per Event | 3.71 |
| Maximum Actions per Event | 13 |
| Dataset Size | 109.4 MB |

---

# Dataset Structure

The main dataset file is: SmartHomeIoTNLU.csv

Each row represents: One natural language command + Context information + One device-action pair


---

# Dataset Schema

| Attribute | Description |
|---|---|
| Event_ID | Unique identifier linking multiple device actions belonging to one event |
| Intent_Type | Interaction intent category |
| Command | Natural language user command |
| Device | Target IoT device |
| Current State | Device state before execution |
| Time | Time context (Morning, Noon, Afternoon, Evening, Night) |
| Light | Ambient light percentage |
| Temperature | Ambient temperature |
| Noise | Environmental noise level |
| Occupancy | Number of occupants |
| Location | Smart home room |
| Scenario | Activity scenario |
| Action | Executable device action |
| Parameters | Optional device-specific control parameters |

---

# Event-Level Representation

SmartHomeIoTNLU follows a hierarchical event-based structure.

A single user command may generate multiple coordinated device actions.

For example:
Event_ID:
4635f6a5-7bf5-4199-9016-52f750d58c91

Command:
"I want to eat now"

Time : Noon

Temperature : 23°C

Location: Dining Room

Generated actions:

| Device | Action |
|---|---|
| Air Purifier | ON |
| Radio | ON |
| Curtains | OPEN |
| Light | ON |
| Water Dispenser | ON |
| AC | ADJUST | Temp=24°C  |

Multiple rows with the same `Event_ID` represent one complete smart home event.

This design enables:

- Row-level learning
- Event-level learning
- Multi-device reasoning
- Sequence modelling
- Context-aware decision making

**Important:** Duplicate `Event_ID` values are expected and represent coordinated multi-device interactions. They should not be removed during preprocessing.

---

# Intent Types

SmartHomeIoTNLU contains two main interaction categories.

## 1. Direct Device Control

Commands targeting individual IoT devices.

Examples: Turn on the bedroom light, Switch off the television, Open the curtains


---

## 2. Scene Control

Commands requiring coordinated actions across multiple devices.

Examples: Prepare my room for sleeping, Clean the kitchen, Activate eating mode


---

# Supported Machine Learning Tasks

## 1. Intent Classification

### Input
Command + Context

### Output
Intent_Type

Example: "Prepare my bedroom for sleeping"
↓
Scene_Control


---

## 2. Device Action Prediction

### Input

Command + Context

### Output

Device-action pairs

Example: Clean the living room
↓
Robot Vacuum → ON
Mop Robot → ON
Curtains → OPEN

---

## 3. Parameter Prediction

### Input
Command + Environmental Context

### Output
Device parameters

Example:
AC → Target Temperature


---

## Dataset Files

Repository structure:

```text
SmartHomeIoTNLU/
├── dataset/
│   ├── SmartHomeIoTNLU.csv
│   ├── ConverterToJSON.ipynb
│   ├── train.json
│   ├── validation.json
│   └── test.json
│
├── notebooks/
│   ├── dataset_overview_validation_distribution_analysis.ipynb
│   └── baseline_models.ipynb
│
├── results/
│   ├── figures/
│   └── tables/
│
├── requirements.txt
├── README.md
└── LICENSE
```


---

# Dataset Splitting

The dataset provides predefined splits:

- Training: 70%
- Validation: 15%
- Test: 15%

Splitting is performed at the **Event_ID level** to prevent information leakage between device actions belonging to the same smart home event. Also, consider commands when wanting to perform natural language understanding to ensure each partition has unseen commands

---

# Validation and Quality Checks

The dataset includes validation procedures to verify:

- Missing required values
- Event-level consistency
- Valid device-action mappings
- Context completeness
- Parameter consistency
- Label coverage

Validation results and generated tables are available in: results/


---

# Dataset Analysis

The repository includes notebooks for reproducing dataset analysis:

## Dataset Overview
dataset_overview & validation & distribution_analysis.ipynb

Provides:

- Dataset statistics
- Schema inspection
- Basic analysis
- Data integrity checks
- Validation reports

Generates:

- Time distribution
- Scenario distribution
- Device distribution
- Action distribution
- Event complexity analysis

## Baseline Models
baseline_models.ipynb


Provides examples for:

- Intent classification
- Multi-label device-action prediction
- Parameter prediction

---

# Installation

Install required Python packages:

bash
pip install -r requirements.txt

---


# Creation

SmartHomeIoTNLU was created using a synthetic dataset generation framework consisting of:

Natural language command generation
Context generation
Device-action mapping
Parameter generation
Dataset validation

The complete dataset generation framework will be released after publication of the associated IEEE Data Descriptor paper.

---

# Citation

If you use SmartHomeIoTNLU in your research, please cite the associated
dataset descriptor paper:


@dataset{mgimba2026smarthomeiotnlu,
  author = {Mgimba, Belnadino and Jindal, Anish},
  title = {SmartHomeIoTNLU: A Context-Rich Smart Home Dataset for Natural Language Understanding and Coordinated Multi-Device IoT Control},
  year = {2026},
  publisher = {GitHub},
  version = {1.0}
}

---

# Acknowledgements

This dataset was developed at:

Department of Computer Science
Durham University
United Kingdom

Supported by:

Durham University
Tanzania Communication Regulatory Authority (TCRA)


---

# License

SmartHomeIoTNLU is released under the Creative Commons Attribution 4.0
International (CC BY 4.0) License.

Users are free to share and adapt the dataset provided that appropriate
credit is given to the authors.

See the LICENSE file for full details.


# Contact

For questions, feedback, or research collaboration:

Belnadino Mgimba,
Department of Computer Science,
Durham University, United Kingdom

Email: belnadinomgimba@gmail.com
