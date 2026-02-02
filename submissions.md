10 Academy: TRP   








TRP 1 - AI-Content Generation Challenge





Samrawit Zerfu Assefa
February 02 2026









Environment Setup Documentation

Which APIs did you configure?
I used both Google Gemini and AIMLAPI 
Any issues encountered during setup?
It worked well on the setup,
How did you resolve them?
I tried adding a lyrics document, tried to fill in fake credit card information, but it didn’t work. 

Codebase Understanding

Architecture diagram or description
The codebase is organized around a modular provider system for generating AI content (like music or images). You can see the folder structure and description of each folder. 

trp1-ai-artist/
├─ src/
│  ├─ ai_content/              # Core library for AI content generation
│  │  ├─ cli/                  # Command-line interface
│  │  ├─ providers/            # Different AI providers (MiniMax, Lyria, etc.)
│  │  │  ├─ aimlapi/           # AIMLAPI-based providers
│  │  │  │  └─ minimax.py      # Music generation via MiniMax
│  │  ├─ core/                 # Shared utilities and base classes
│  │  │  └─ client.py          # Base HTTP client for AIMLAPI
│  │  └─ config.py             # Configuration and API keys
├─ .env                        # Environment variables and API keys
└─ main.py / CLI commands      # Entry points for generating music

Key insights about the provider system
Providers are organized by AI platform (like Google, AIMLAPI, Kling). Inside each platform folder, there are Python files for each provider: imagen.py for image generation, lyria.py for music generation, and veo.py for video generation. Each provider is a class with a generate() function and is registered in the core registry.
Music Providers:
Lyria – Real-time streaming, instrumental only, supports BPM and temperature control, no vocals/lyrics.
MiniMax – Supports vocals/lyrics and lyrics-first workflows, can generate music based on lyrics.


Differences: Lyria is fast, real-time, and instrumental-focused, while MiniMax can handle vocals and structured lyrics.
Video Providers:
Veo – Text-to-video and image-to-video generation, supports multiple aspect ratios.
Supports Image-to-Video: Veo (can animate a keyframe image).
Provider Supporting Vocals/Lyrics: MiniMax (Lyria does not).
 3. Preset System
Music Presets
From presets/music.py (via MUSIC_PRESETS):
Preset Name
BPM
Mood / Style Example
jazz
120
Smooth, instrumental, jazz fusion
pop
100
Upbeat, vocals-friendly
(others)
varies
Defined in MUSIC_PRESETS dictionary

Video Presets
From presets/video.py (via VIDEO_PRESETS):
Preset Name
Aspect Ratio
Style / Example
nature
16:9
Scenic, cinematic nature scenes
urban
16:9
City scenes, dynamic motion
portrait
9:16
Vertical format
square
1:1
Social media / Instagram style


How the pipeline orchestration works
The pipelines/ directory organizes workflows that combine multiple content generation steps—music, image, and video—into end-to-end processes. It manages execution, handles parallel tasks, merges outputs, and provides ready-to-use pipeline strategies like music-first, lyrics-first, text-to-video, or image-to-video.


Generation Log

Commands executed
Clone the repository
git clone https://github.com/10xac/trp1-ai-artist.git – 
cd trp1-ai-artist 
Set up environment variables
cp .env.example .env
Sync project dependencies
uv sync
Check available commands
uv run ai-content --help
Generate music using Lyria
uv run ai-content music --style jazz --provider lyria
List available providers
uv run ai-content list-providers 
List preset styles
 uv run ai-content list-presets
Generate music with duration
uv run ai-content music --style jazz --provider lyria --duration 30
Run an example script
uv run python examples/lyria_example_ethiopian.py --style ethio-jazz --duration 30


Prompts used and why

Prompt
Why It Was Used
"jazz"
To generate a general jazz music track — tests basic functionality of the provider.
"ethio-jazz"
To generate Ethiopian jazz music — demonstrates regional or cultural style capabilities of the AI.
"eskista-dance"
To generate a traditional Ethiopian dance rhythm — tests provider’s ability to handle specific cultural styles.
"Smooth jazz fusion instrumental"
To test generating instrumental music with a fusion/jazz style without lyrics.


Results achieved (screenshots, file sizes, durations)




Image showing result showing output of uv run ai-content list-providers and uv run ai-content list-presets


Image showing  output of uv run ai-content --help command 



Image showing the results of content creation - audio 



Image showing the output of uv run python examples/lyria_example_ethiopian.py --style ethio-jazz --duration 30
Challenges & Solutions

What didn't work on first try?
Because I don’t have a credit card information. 
How did you troubleshoot?
tried to write my own lyrics
tired of changing providers - Google Gemini, and AIMLAPI 
Changed my commands 
What workarounds did you discover?
I think filling in the credit card information might give me a free quota to process my commands. 

Insights & Learnings

What surprised you about the codebase?
The code is well-structured and uses a central client (AIMLAPIClient) for all API calls, so different music providers like MiniMax or Lyria share the same logic.
I was surprised by how the system supports multiple providers and styles, and even allows reference audio and lyrics for music generation.
The pipeline uses async programming so it can handle waiting for music generation without blocking other tasks — this was neat and efficient.

What would you improve?
Make it easier to generate instrumental music without needing lyrics. Right now, some providers force you to provide text.
Add better error messages for quota limits and verification issues. This would save time troubleshooting.
Include more examples and presets for cultural music styles, so users can test quickly without creating their own prompts.

How does this compare to other AI tools you've used?
Unlike many AI tools that are single-purpose, this system is flexible: you can switch providers, styles, durations, and even add lyrics or reference audio.
The async pipeline is better than some older AI tools that block until results are ready.
Error handling and verification requirements can be stricter, so it feels more professional but also more restrictive than some open-access AI music platforms.



Links

YouTube video link(s) - I didn’t generate any video 
GitHub repo with your exploration artifacts -  https://github.com/Samrizee/trp1-ai-artist.git



