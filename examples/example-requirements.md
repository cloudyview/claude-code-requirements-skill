# AI Dubbing System — Requirements

> Created: 2026-03-06
> Status: Complete

## 1. Feature Overview
- Automatic voice dubbing for video clips using AI text-to-speech
- Support multiple voice styles per character
- Sync audio timing with video scene duration
- Preview dubbing result before finalizing

## 2. User Stories
- As a video producer, I want to assign voice profiles to characters so each character sounds consistent across episodes
- As an editor, I want to preview AI-generated voiceover before committing it to the timeline
- As a director, I want to adjust voice emotion (happy, sad, angry) per scene

## 3. Core Requirements
- **Voice Assignment**: Map characters (from Asset system) to voice profiles
- **Batch Generation**: Generate voiceover for all dialogue lines in an episode at once
- **Emotion Control**: Support at least 5 emotion presets per voice
- **Timing Sync**: Auto-adjust speech speed to fit scene duration
- **Preview Player**: Inline audio player with waveform visualization
- **Export**: Separate audio tracks per character for mixing

## 4. Interaction Design
- Entry point: "Dubbing" tab in the Render module
- Left panel: Scene list with dialogue lines
- Right panel: Voice assignment + preview player
- Batch mode: Select multiple scenes → "Generate All" button
- Progress shown in Global Production Monitor (existing Workstation system)

## 5. Data Model
- **VoiceProfile**: id, name, provider, voiceId, emotion, speed, pitch
- **DubbingJob**: id, projectId, episodeId, sceneId, characterId, voiceProfileId, dialogueText, audioRef, status, duration
- Relations: Character (Asset) → VoiceProfile (1:many), Scene → DubbingJob (1:many)

## 6. Technical Constraints
- TTS providers: Initially support Google Cloud TTS and ElevenLabs
- Audio format: WAV for editing, MP3 for preview
- Max 50 concurrent TTS API calls (rate limiting)
- Must integrate with existing Workstation queue system

## 7. Open Questions
- [Resolved] Q: Should we support custom voice cloning? A: Not in v1, add as future enhancement
- [Resolved] Q: How to handle scenes with overlapping dialogue? A: Generate separate tracks, let user mix in timeline

## 8. Implementation Notes
- Reuse `services/llm/render.ts` pattern for TTS API calls
- Voice profiles can extend existing `Asset` model (type: 'VOICE')
- Dubbing jobs follow `Shot` status pattern (PENDING → QUEUED → RENDERING → COMPLETED)
- UI follows existing Render module layout pattern
- Queue management through existing `useWorkstation()` hook
