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

### Claude Code as Bridge

These days I'm using Claude Code (Claude CLI) constantly for local system optimization and operation. I'm using it not necessarily for what it's actually built for, but as a control interface for the computer - like "can we check why ComfyUI isn't launching?"

**This is a huge step towards making this idea feasible and viable** - it's an excellent bridge between natural language and executing commands.

### Agentic vs Visual Approaches

I've used visual-based approaches with computer vision and object detection, but haven't had much success. The agentic level operating at the command execution level has been **much more reliable and successful**.

It avoids complications of:
- Taking screen grabs to understand the screen
- Privacy risks (which make me quite uncomfortable)

I'm already using Claude as that intermediary on my 12GB VRAM machine.

## The Ideal Unified Solution

### Why Unity Matters

I think this has to be a **unified solution** for voice. I don't want:
- A voice keyboard up AND
- A voice control tool up

They overlap in terms of VAD (Voice Activity Detection) and can't coexist easily. It's better to have one voice module doing all these things than trying to run two things in parallel that will conflict.

### The Complete Workflow

The ideal situation would be running as a boot process with seamless flow:

1. **Command execution phase:** "Open my personal Chrome, go to this website, open email to this person"
2. **Dictation phase:** Shift seamlessly into typing/dictation
3. **Return to commands:** Move on to next task
4. **Meeting mode:** Pause command with "go to sleep" - stop wake word detection during meetings
5. **Resume:** Back to commands and dictation after meeting
6. **All the way through:** To turning off or snoozing the computer

This would encompass probably **99% of the workday**.

## Next Steps

I'd love to get a sense of what's currently available in terms of:
- Computer control technologies
- Computer use technologies

Then I can make a better informed decision about how to get from A to B. The ultimate tool I'm looking for may need to be cobbled together myself, in which case these notes serve as context data and spec notes for bringing together these components into one cohesive system.

---

*Transcription confidence: 96.7%*
