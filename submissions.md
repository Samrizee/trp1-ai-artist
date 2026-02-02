Package Structure
What are the main modules in src/ai_content/?
The main modules in src/ai_content/ are:
cli/ – Command-line interface scripts to run the package from the terminal.
core/ – Core framework of the package, including:
registry.py (provider registry)
result.py (GenerationResult class)
exceptions.py (custom errors like ProviderError)
config/ or config.py – Configuration settings, like API keys, model names, and output directories.
integrations/ – Optional connectors to external tools or services.
pipelines/ – Defines workflows for generating content (images, music, video) using providers and presets.
presets/ – Stores predefined music and video settings (BPM, mood, aspect ratios).
providers/ – Contains the AI provider classes (Imagen, Lyria, Veo) that generate the actual content.
utils/ – Helper functions used across the package.
How are providers organized?
Providers are organized by AI platform (like Google, AIMLAPI, Kling). Inside each platform folder, there are Python files for each provider: imagen.py for image generation, lyria.py for music generation, and veo.py for video generation. Each provider is a class with a generate() function and is registered in the core registry.
What is the purpose of the pipelines/ directory?
The pipelines/ directory organizes workflows that combine multiple content generation steps—music, image, and video—into end-to-end processes. It manages execution, handles parallel tasks, merges outputs, and provides ready-to-use pipeline strategies like music-first, lyrics-first, text-to-video, or image-to-video.

2. Provider Capabilities
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

How to Add a New Preset
Open the relevant preset file:
Music → presets/music.py
Video → presets/video.py


Add a new entry in the dictionary (MUSIC_PRESETS or VIDEO_PRESETS), for example:


Music example:
MUSIC_PRESETS["lofi"] = Preset(
    prompt="Chill lofi beats, smooth instrumental",
    bpm=85
)

Video example:
VIDEO_PRESETS["sunset"] = VideoPreset(
    prompt="Sunset over mountains, cinematic view",
    aspect_ratio="16:9"
)

Save the file — the new preset is immediately available for pipelines using get_preset("lofi") or get_preset("sunset").
4.  CLI Commands
What commands are available?
music – Generate music using presets and providers.
video – Generate video from text or image.
full – Run the full content pipeline (music + image + video merge).
list – List available presets or providers.
What options does the music command accept?
--style – Music preset name (e.g., jazz, pop).
--provider – Music provider (lyria, minimax).
--duration – Length of music in seconds.
--bpm – Override BPM from preset.
--lyrics – Input lyrics (only works if provider supports vocals).
What options does the video command accept?
--style – Video preset name (e.g., nature, urban).
--provider – Video provider (veo).
--aspect-ratio – Video aspect ratio (16:9, 9:16, 1:1).
--duration – Length of video in seconds.
--keyframe – Path to image for image-to-video generation.
--prompt – Custom text prompt (overrides preset).



