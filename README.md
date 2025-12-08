> ** SCL code generation and debugging for Siemens S7-1500/S7-1200 PLCs using GitHub Copilot Agents**

[![TIA Portal](https://img.shields.io/badge/TIA%20Portal-Compatible-009999?style=flat-square)](https://www.siemens.com/tia-portal)
[![S7-1500](https://img.shields.io/badge/S7--1500-Supported-009999?style=flat-square)](https://www.siemens.com)
[![S7-1200](https://img.shields.io/badge/S7--1200-Supported-009999?style=flat-square)](https://www.siemens.com)
[![SCL](https://img.shields.io/badge/Language-SCL-blue?style=flat-square)](https://www.siemens.com)
[![GitHub Copilot](https://img.shields.io/badge/GitHub%20Copilot-Agents-purple?style=flat-square)](https://github.com/features/copilot)

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Available Agents](#-available-agents)
- [Knowledge Base](#-knowledge-base)
- [Coding Standards](#-coding-standards)
- [Usage Examples](#-usage-examples)
- [Best Practices](#-best-practices)
- [Contributing](#-contributing)
- [License](#-license)

## 🎯 Overview

This repository provides a comprehensive **GitHub Copilot Agent workspace** for developing Siemens PLC code using **Structured Control Language (SCL)** in TIA Portal. It includes specialized AI agents, coding guidelines, and extensive knowledge bases to accelerate PLC software development with best practices and industry standards.

### Why This Repository?

- **🤖 AI-Powered Development**: Leverage GitHub Copilot agents specifically trained for SCL programming
- **📚 Comprehensive Knowledge Base**: Access 12,000+ lines of SCL documentation, 244+ instructions, and LGF library references
- **✅ Enforced Best Practices**: Automatic adherence to Siemens coding standards and naming conventions
- **🐛 Intelligent Debugging**: Automated code review and bug detection for SCL code
- **⚡ Rapid Development**: Generate production-ready SCL code with proper structure and documentation

## ✨ Features

### Core Capabilities

- ✅ **SCL Code Generation** - Generate Functions, Function Blocks, Data Blocks, and User-Defined Types
- ✅ **Automated Code Review** - Comprehensive debugging and static analysis
- ✅ **LGF Library Integration** - Utilize Siemens Library of General Functions
- ✅ **Naming Convention Enforcement** - Automatic compliance with PascalCase, snake_case, and prefixing standards
- ✅ **S7-1500/S7-1200 Compatibility** - Ensure code works on target PLC families
- ✅ **Documentation Generation** - Auto-generate inline documentation and comments
- ✅ **Edge Case Handling** - Built-in validation for array bounds, data types, and error conditions

### Supported PLC Families

| PLC Family | Support Status | Notes |
|------------|----------------|-------|
| **S7-1500** | ✅ Full Support | All features available |
| **S7-1200** | ✅ Full Support | Instruction compatibility verified |
| **Safety PLCs (F-CPU)** | ❌ Not Supported | Out of scope |

## 📁 Repository Structure

```
Github_Copilot_SCL_Siemens_TIA/
├── .github/
│   ├── agents/
│   │   ├── SCL_TIA_Portal_Coding.agent.md    # Main SCL coding agent
│   │   └── SCL_Debbuger_Agent.agent.md       # Code review & debugging agent
│   │
│   ├── instructions/
│   │   └── Siemens_SCL_TIA_Portal.instructions.md  # Coding guidelines (457 lines)
│   │
│   └── knowledge-bases/
│       └── Siemens_SCL_TIA_Portal/
│           ├── scl_keywords.md               # 244+ SCL instructions (12,383 lines)
│           ├── scl_instruction_details.md    # Detailed instruction reference (5,333 lines)
│           └── siemens_LGF.md                # LGF library documentation (7,204 lines)
│
├── .gitignore
├── .vscode/                                   # VS Code workspace settings
└── README.md                                  # This file
```

## 🚀 Getting Started

### Prerequisites

- **VS Code** with GitHub Copilot extension installed
- **GitHub Copilot subscription** (required for agent features)
- **TIA Portal V16+** (for testing generated code)
- Basic understanding of **PLC programming** and **SCL syntax**

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/rtmachines/Github_Copilot_SCL_Siemens_TIA.git
   cd Github_Copilot_SCL_Siemens_TIA
   ```

2. **Open in VS Code**
   ```bash
   code .
   ```

3. **Activate GitHub Copilot**
   - Ensure GitHub Copilot is enabled in VS Code
   - Verify agents are available in the Copilot Chat panel

4. **Start coding!**
   - Open Copilot Chat (`Ctrl+Shift+I`)
   - Reference agents using `@SCL_TIA_Portal_Coding` or `@SCL_Debbuger_Agent`

## 🤖 Available Agents

### 1. SCL TIA Portal Coding Agent
**File**: `.github/agents/SCL_TIA_Portal_Coding.agent.md`

**Purpose**: Generate production-ready SCL code for Siemens PLCs

**Capabilities**:
- ✅ Generate Functions (`FC_*.scl`)
- ✅ Generate Function Blocks (`FB_*.scl`)
- ✅ Generate Data Blocks (`DB_*.scl`)
- ✅ Generate User-Defined Types (`T_*.udt`)
- ✅ Code optimization and refactoring
- ✅ Migration from other PLC languages

**Example Usage**:
```
@SCL_TIA_Portal_Coding Create a motor control function block with start/stop logic, 
speed control, and error handling for S7-1500
```

**Workflow**:
1. Reads coding instructions and knowledge base
2. Analyzes requirements and asks clarifying questions
3. Searches for relevant LGF functions and examples
4. Generates code following standards
5. Verifies PLC compatibility

### 2. SCL Debugger Agent
**File**: `.github/agents/SCL_Debbuger_Agent.agent.md`

**Purpose**: Automated code review and bug detection

**Analysis Areas**:
- ✅ Syntax and compilation issues
- ✅ Logic errors (division by zero, array bounds, infinite loops)
- ✅ Data type compatibility and conversions
- ✅ Control flow analysis (unreachable code, return paths)
- ✅ SCL-specific issues (memory areas, timers, strings)
- ✅ Performance optimization opportunities
- ✅ Safety and robustness checks
- ✅ Best practices compliance

**Example Usage**:
```
@SCL_Debbuger_Agent Review this function block for potential bugs and optimization opportunities
```

**Output Format**: Structured report with Critical ❌, Major ⚠️, Minor ℹ️ issues, edge cases 🔍, and optimization suggestions 🚀

## 📚 Knowledge Base

### SCL Keywords Reference
**File**: `.github/knowledge-bases/Siemens_SCL_TIA_Portal/scl_keywords.md`
- **12,383 lines** of comprehensive documentation
- **244+ instructions** organized by category
- **10 categories**: Arithmetic, Bit Operations, Counters, Data Conversion, Memory, Timers, etc.

### SCL Instruction Details
**File**: `.github/knowledge-bases/Siemens_SCL_TIA_Portal/scl_instruction_details.md`
- **5,333 lines** of detailed implementation guides
- **165+ instructions** with parameters and examples
- Categories include Arithmetic, Bit Operations, Comparison, Counters, Edge Detection, Memory, Strings, Timers

### Siemens LGF Library
**File**: `.github/knowledge-bases/Siemens_SCL_TIA_Portal/siemens_LGF.md`
- **7,204 lines** of LGF library documentation
- **50+ library functions** for common tasks
- Categories:
  - Array Processing (search, sort, analyze)
  - Mathematical Functions (factorial, random, regression)
  - Data Type Conversion (string, time, number)
  - Bit/Byte Manipulation
  - Time and Date Functions
  - String Processing
  - CRC Calculation (CRC8, CRC16, CRC32)
  - Matrix Operations
  - Statistical Analysis
  - Advanced Functions (ramps, buffers)

## 📝 Coding Standards

### Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| **Variables (non-temp)** | PascalCase | `MotorSpeed`, `TemperatureThreshold` |
| **Variables (in functions)** | snake_case with `_` prefix | `_motor_speed`, `_temperature_threshold` |
| **Constants** | UPPER_SNAKE_CASE | `MAX_PRESSURE`, `DEFAULT_TIMEOUT` |
| **Functions** | PascalCase | `CalculateArea`, `GetSensorData` |
| **Function Blocks** | `FB_` + PascalCase | `FB_MotorControl`, `FB_TempMonitor` |
| **Input Parameters** | `i` + PascalCase | `iSensorValue`, `iConfigData` |
| **Output Parameters** | `o` + PascalCase | `oActuatorState`, `oErrorCode` |
| **In/Out Parameters** | `io` + PascalCase | `ioConfigurationData` |
| **Booleans** | Is/Has/Can/Should prefix | `IsActive`, `HasError`, `CanStart` |
| **Temporary Variables** | `_t_` + snake_case | `_t_temp_result`, `_t_index` |
| **Global Variables** | `Glb_` + PascalCase | `Glb_SystemStatus` |
| **Data Blocks** | `DB_` + PascalCase | `DB_MotorData` |
| **User Defined Types** | `T_` + PascalCase | `T_MotorType` |
| **FB Instances** | `_` + PascalCase | `_MotorControl`, `_TempMonitor` |
| **Configuration Variables** | `Cfg_` after prefix | `Cfg_MaxSpeed`, `iCfg_Timeout` |
| **State Machine States** | `STATE_` + UPPER | `STATE_IDLE`, `STATE_RUNNING` |
| **Edge Detection** | RisingEdge/FallingEdge | `_t_RisingEdge_Start` |

### Best Practices

✅ **DO**:
- Use IEC standard timers/counters for portability
- Optimize data blocks with `S7_Optimized_Access := 'TRUE'`
- Use DINT for loop counters and state machines
- Implement state machines for complex process control
- Validate inputs and handle edge cases
- Use temporary variables (VAR_TEMP) for local calculations
- Prefer LGF library functions for common tasks
- Initialize all variables to avoid undefined states
- Use symbolic names for hardware addresses

❌ **DON'T**:
- Use deep nesting of IF statements (use CASE instead)
- Use magic numbers (define constants)
- Create long blocking operations (use state machines)
- Overuse global variables (pass parameters instead)
- Ignore scan cycle time implications
- Create unnamed or unclear variable names

## 💡 Usage Examples

### Example 1: Generate a Motor Control Function Block

**Prompt**:
```
@SCL_TIA_Portal_Coding Create a function block for motor control with:
- Start/Stop commands
- Speed setpoint (0-100%)
- Emergency stop input
- Running status output
- Error handling with error codes
- Compatible with S7-1500
```

**Generated Output** (FB_MotorControl.scl):
```scl
FUNCTION_BLOCK "FB_MotorControl"
{ S7_Optimized_Access := 'TRUE' }
VERSION : 0.1
   VAR_INPUT 
      iStart : Bool;   // Start command
      iStop : Bool;   // Stop command
      iEmergencyStop : Bool;   // Emergency stop input
      iSpeedSetpoint : Real;   // Speed setpoint (0.0 to 100.0%)
   END_VAR

   VAR_OUTPUT 
      oIsRunning : Bool;   // Motor running status
      oHasError : Bool;   // Error flag
      oErrorCode : DInt;   // Error code
      oActualSpeed : Real;   // Actual speed output (0.0 to 100.0%)
   END_VAR

   VAR 
      State : DInt;   // State machine state
      SpeedPrev : Real;   // Previous speed value
      _TON_StartDelay : TON;   // Start delay timer
   END_VAR

   VAR_TEMP 
      _t_valid_setpoint : Bool;
   END_VAR

   VAR CONSTANT 
      STATE_IDLE : DInt := 0;
      STATE_STARTING : DInt := 1;
      STATE_RUNNING : DInt := 2;
      STATE_STOPPING : DInt := 3;
      STATE_ERROR : DInt := 99;
      
      ERR_INVALID_SETPOINT : DInt := 1001;
      ERR_EMERGENCY_STOP : DInt := 1002;
   END_VAR

BEGIN
   // Input validation
   _t_valid_setpoint := (iSpeedSetpoint >= 0.0) AND (iSpeedSetpoint <= 100.0);
   
   // State machine implementation
   // ... (rest of implementation)
   
END_FUNCTION_BLOCK
```

### Example 2: Debug Existing Code

**Prompt**:
```
@SCL_Debbuger_Agent Analyze this code for potential issues:

FUNCTION_BLOCK "FB_Test"
VAR_INPUT
   iValue : Int;
END_VAR
VAR
   Result : Real;
END_VAR
BEGIN
   Result := 100 / iValue;
END_FUNCTION_BLOCK
```

**Agent Response**:
```markdown
# Debug Analysis Report

## Executive Summary
Found 1 critical issue, 1 major issue, and 2 minor issues

## Critical Issues ❌

### Issue 1: Division by Zero Risk
- **Location**: Line 8
- **Severity**: Critical
- **Description**: Division operation without checking if divisor is zero
- **Impact**: Runtime error if iValue = 0
- **Recommended Fix**:
  IF iValue <> 0 THEN
      Result := 100.0 / INT_TO_REAL(iValue);
  ELSE
      Result := 0.0;
      // Set error flag
  END_IF;

## Major Issues ⚠️

### Issue 1: Implicit Type Conversion
- **Location**: Line 8  
- **Severity**: Major
- **Description**: Dividing integer by integer then assigning to Real may lose precision
- **Recommended Fix**: Convert iValue to REAL before division
```

### Example 3: Use LGF Library Function

**Prompt**:
```
@SCL_TIA_Portal_Coding I need to find the minimum and maximum values 
in an array of UDInt values. Use LGF library if available.
```

**Agent Response**:
```scl
// Using LGF_SearchMinMax_UDInt from Siemens LGF library

FUNCTION "FC_FindArrayMinMax" : Void
VAR_INPUT 
   iValues : Array[0..99] of UDInt;   // Input array
END_VAR

VAR_OUTPUT 
   oMinValue : UDInt;   // Minimum value found
   oMinIndex : DInt;   // Index of minimum value
   oMaxValue : UDInt;   // Maximum value found
   oMaxIndex : DInt;   // Index of maximum value
END_VAR

BEGIN
   // Call LGF library function for efficient min/max search
   "LGF_SearchMinMax_UDInt"(
      values := #iValues,
      minValue => #oMinValue,
      minValueIndex => #oMinIndex,
      maxValue => #oMaxValue,
      maxValueIndex => #oMaxIndex
   );
END_FUNCTION
```

## 🎓 Best Practices

### When to Use Each Agent

| Scenario | Agent to Use | Why |
|----------|--------------|-----|
| New code generation | `@SCL_TIA_Portal_Coding` | Follows standards, uses knowledge base |
| Code review | `@SCL_Debbuger_Agent` | Comprehensive analysis |
| Optimization | Both agents | Coding agent for refactoring, debugger for analysis |
| Migration | `@SCL_TIA_Portal_Coding` | Ensures SCL compatibility |
| Learning SCL | `@SCL_TIA_Portal_Coding` | Generates well-documented examples |

### Development Workflow

1. **Planning Phase**
   - Define requirements clearly
   - Identify which LGF functions might be useful
   - Consult knowledge base for available instructions

2. **Generation Phase**
   - Use `@SCL_TIA_Portal_Coding` with detailed prompts
   - Review generated code structure
   - Verify naming conventions are followed

3. **Review Phase**
   - Run `@SCL_Debbuger_Agent` on generated code
   - Address critical and major issues
   - Consider optimization suggestions

4. **Testing Phase**
   - Import code into TIA Portal
   - Compile and verify no errors
   - Test edge cases identified by debugger agent

5. **Documentation Phase**
   - Ensure inline comments are clear
   - Add function/FB descriptions
   - Document any assumptions or limitations

## 🛠️ Advanced Features

### Supported File Types

| Extension | Purpose | Agent Support |
|-----------|---------|---------------|
| `.scl` | SCL source files (FC, FB) | ✅ Full |
| `.udt` | User-Defined Types | ✅ Full |
| `.db` | Data Block definitions | ✅ Full |

### Integration with TIA Portal

1. **Export from Agent**
   - Copy generated SCL code
   - Create new block in TIA Portal
   - Paste code into SCL editor

2. **Import to Agent for Review**
   - Copy existing SCL code from TIA Portal
   - Paste in VS Code
   - Run `@SCL_Debbuger_Agent` for analysis

3. **Iterative Development**
   - Generate initial version with coding agent
   - Import to TIA Portal and test
   - Export issues back to VS Code
   - Use debugger agent to identify problems
   - Regenerate with coding agent

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/AmazingFeature`)
3. **Add knowledge base entries** for new SCL instructions or LGF functions
4. **Update documentation** if adding new agents or guidelines
5. **Commit changes** (`git commit -m 'Add some AmazingFeature'`)
6. **Push to branch** (`git push origin feature/AmazingFeature`)
7. **Open a Pull Request**

### What to Contribute

- ✅ New SCL instruction documentation
- ✅ Additional LGF function examples
- ✅ Code templates and snippets
- ✅ Bug fixes in knowledge base
- ✅ Improved coding guidelines
- ✅ Real-world usage examples

## 📄 License

This project is provided as-is for educational development purposes. 

**Note**: Siemens, TIA Portal, S7-1500, S7-1200, and SCL are trademarks of Siemens AG. This repository is not affiliated with or endorsed by Siemens AG.

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/rtmachines/Github_Copilot_SCL_Siemens_TIA/issues)
- **Discussions**: [GitHub Discussions](https://github.com/rtmachines/Github_Copilot_SCL_Siemens_TIA/discussions)

## 🔗 Resources

- [Siemens TIA Portal](https://www.siemens.com/tia-portal)
- [SCL Programming Guide](https://support.industry.siemens.com/)
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [S7-1500 Manual](https://support.industry.siemens.com/)

## 🏆 Acknowledgments

- Siemens AG for TIA Portal and SCL language
- GitHub for Copilot AI capabilities
- PLC programming community for best practices
