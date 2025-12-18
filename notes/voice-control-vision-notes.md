# Voice Control for Linux - Vision and Requirements

**Date:** December 18, 2025
**Purpose:** Context data describing the aspirational target for voice control technology on Linux

## Current State - Voice Typing

I've discovered over the last year of intensive voice tech use that I have solutions for voice typing. They're not perfect, but they are a large part of the way towards what I'm looking for.

### Custom Voice Notepad Solution

I've created my own tool for voice note taking using Gemini Google multimodal. The utility of this over using Whisper alone is very significant for my use case.

#### Layered Approach to Text Processing

Instead of just directly capturing text with all verbal tics ("you know", "um", etc.), I've implemented a multi-layer approach:

**Layer 1: Text Cleaning/Sanitization**
- Removing filler words
- Removing "ums" and other verbal tics
- Removing unnecessary elements from transcript

**Layer 2: Stylistic Edits**
- Formal vs informal tone
- Context-appropriate style (interpersonal communication for friends should be informal)

**Layer 3: Tone Adjustments**
- More enthusiastic
- More persuasive
- Other emotional/rhetorical adjustments

### Current Success Level

This implementation has worked extremely well at the note level. I've had proof of concept success that relieves me of 70-80% of typing needs:
- Don't need to type emails
- Don't need to type notes
- Can use voice to capture text

The app even includes user settings for name/signature, so when choosing email as target format, it includes my signature automatically.

### Virtual Keyboard Challenge

Getting virtual keyboard input working is the hard part. For obvious security reasons, keyboard entry at the OS level is very sensitive and can be used maliciously. This makes it challenging to get virtual input keyboard to work as desired.

I've seen it work with the Deepgram Linux voice keyboard utility, but it's been challenging. What I want is the ability to type into any field in the computer, and while that level of operation is possible, implementation has been difficult.

## The Gap - Voice Control

What my current solution doesn't do, and what I'm looking for as the accessory component, is **the ability to control the computer**.

### Critical Requirement: OS-Level Implementation

**This must operate at the OS level, not within the browser.** Browser-based voice control solutions are fundamentally limited - they only work within the browser context. For system control, we need to go far beyond that scope.

The requirement is for:
- System-wide voice control across all applications
- Ability to control the desktop environment, file manager, terminal
- Control over multiple applications simultaneously (code editor, multiple Chrome profiles, etc.)
- Full OS integration, not siloed within a single application context

### My Working Environment

- **OS:** Ubuntu 25.10
- **Setup:** Three screens (daily workstation where 80% of work gets done)
  - Left screen: Code editor
  - Center screen: Personal Chrome profile
  - Right screen: Work Chrome profile
- **Usage:** Rarely use laptop or phone for work - this desktop is the center of operations

### Desired Voice Control Capabilities

Typical commands would include:
- "Close out the code editor"
- "Open a new tab in the personal Chrome"
- "Open this URL in the personal Chrome profile"
- "Close out the business profile"

### Key Applications

Two tools I'm constantly touching in Linux:
1. File manager
2. Terminal

### Claude Code as Bridge to Natural Language Commands

These days I'm using Claude Code (Claude CLI) constantly for local system optimization and operation. I'm using it not necessarily for what it's actually built for, but as a control interface for the computer - like "can we check why ComfyUI isn't launching?"

**This is a huge step towards making this idea feasible and viable** - it's an excellent bridge between natural language and executing commands.

#### How I'm Using Claude Code Now

I'm working on codebases, but **just as commonly (or probably even more commonly)** I'm using it as a control interface for the computer. This represents a significant paradigm shift - using an AI agent as the intermediary layer between voice commands and system execution.

**Key advantages of this approach:**
- Natural language understanding
- Context-aware command execution
- Ability to handle complex, multi-step operations
- No need for rigid command syntax
- Can troubleshoot and adapt when things don't work as expected

### Agentic Command Execution vs Visual Approaches

This is a critical architectural decision that significantly impacts feasibility and reliability.

#### Visual/Computer Vision Approaches (Tried - Limited Success)

I've experimented with visual-based approaches using:
- Computer vision
- Object detection
- Screen grab analysis

**Results:** Haven't had much success with these methods.

**Problems with visual approaches:**
- Reliability issues - screen interpretation is complex and error-prone
- High computational overhead
- **Privacy concerns** - having something constantly taking screen grabs and analyzing my screen makes me quite uncomfortable
- Fragile - breaks when UI elements change or move
- Complexity in understanding multi-screen setups

#### Agentic/Command Execution Level (Current Approach - Much Better)

The agentic level operating at the **command execution level** has been **much more reliable and successful**.

**Why this works better:**
- Direct system interaction through commands
- No need for visual interpretation
- More robust and predictable
- Lower resource overhead
- Better privacy - no screen capture required
- Works across different desktop environments and themes

**Current implementation:** Already using Claude as that intermediary on my 12GB VRAM machine. While this uses a cloud LLM service, there may be open source alternatives that could fill this role for a fully local solution.

## The Ideal Unified Solution

### Why Unity Matters

I think this has to be a **unified solution** for voice. I don't want:
- A voice keyboard up AND
- A voice control tool up

They overlap in terms of VAD (Voice Activity Detection) and can't coexist easily. It's better to have one voice module doing all these things than trying to run two things in parallel that will conflict.

### The Complete Workflow

The ideal situation would be running as a boot process with seamless flow between command execution and dictation:

#### 1. Command Execution Phase
"Open my personal Chrome, go to this website, open email to this person"

**What happens:**
- System interprets natural language commands
- Executes appropriate system calls
- Manages application launching, window switching, URL navigation
- Differentiates between multiple instances (personal vs work Chrome profiles)

#### 2. Dictation Phase
Seamlessly shift into typing/dictation mode

**What happens:**
- System recognizes context switch from commands to text input
- Virtual keyboard input activates
- Multi-layer text processing engages (cleaning, styling, formatting)
- Text appears in the active field with appropriate formatting

**Key requirement:** Seamless flow between these two phases without manual mode switching.

#### 3. Return to Commands
Move on to next task - system automatically recognizes command context vs dictation context

#### 4. Meeting Mode
Pause functionality: "Go to sleep"

**What happens:**
- Stop wake word detection during meetings
- System goes dormant but remains ready
- No accidental command interpretation during conversations
- Resume with wake phrase when meeting ends

#### 5. Full Day Coverage
Back to commands and dictation cycle all the way through to:
- Turning off the computer
- Snoozing the computer
- End of workday shutdown procedures

**This would encompass probably 99% of the workday** - the only time not covered would be during meetings when the system is in sleep mode.

## Technical Architecture Requirements

### Core Components Needed

1. **Voice Activity Detection (VAD)**
   - Must be efficient and accurate
   - Low latency for responsive interaction
   - Shared between command and dictation modes

2. **Speech-to-Text Engine**
   - High accuracy for command recognition
   - Real-time processing
   - Local processing preferred for privacy

3. **Natural Language Understanding Layer**
   - Interprets commands in context
   - Distinguishes between system commands and dictation
   - Claude Code currently fills this role effectively

4. **System Control Interface**
   - OS-level permissions and capabilities
   - Application launching and management
   - Window focus and switching
   - Multi-display awareness
   - File manager and terminal integration

5. **Virtual Keyboard Integration**
   - Universal input capability (any field, any application)
   - Must overcome OS-level security restrictions
   - Seamless activation when in dictation mode

6. **Text Processing Pipeline**
   - Multi-layer approach as described earlier
   - Real-time processing
   - Context-aware formatting

### Integration Points

- **Boot Process Integration:** Launch as system service
- **Desktop Environment Integration:** KDE Plasma on Wayland in my case
- **Application Awareness:** Understanding current application context
- **Profile Differentiation:** Distinguishing between multiple instances of same application (e.g., personal vs work Chrome)

## Implementation Approach

### Likely Reality: Custom Solution Required

The ultimate tool I'm looking for may need to be **cobbled together myself** from existing components. These notes serve as context data and spec notes for bringing together these components into one cohesive system.

### Key Decision Points

1. **LLM for Natural Language Understanding**
   - Currently: Claude Code via API (cloud-based)
   - Alternative: Local open source LLM (need to evaluate options for 12GB VRAM machine)

2. **STT Engine**
   - Options: Whisper (local), Deepgram (API), others
   - Tradeoff: accuracy vs privacy vs latency vs cost

3. **System Control Framework**
   - Need to evaluate existing Linux automation frameworks
   - May need custom integration layer

## Next Steps

### Research Phase

I'd love to get a sense of what's currently available in terms of:
- **Computer control technologies** for Linux
- **Computer use technologies** and CUA (Computer Use Agents)
- **Voice control frameworks** that operate at OS level
- **Virtual keyboard solutions** that work system-wide on Linux
- **Open source alternatives** to Claude for natural language command interpretation

### Decision Making

After surveying the landscape, I can make a better informed decision about:
- Which existing tools can be integrated
- What needs to be built from scratch
- Whether a fully local solution is viable
- What tradeoffs between cloud and local processing make sense

---

**Related Files:**
- [Raw Transcript](voice-control-vision-notes-raw-transcript.md) - Unedited AssemblyAI transcription
- Audio: `notes.mp3` - Original voice recording

*Transcription confidence: 96.7%*
