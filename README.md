# Inspiration & Changes
After following the discussion around "Finetuning Base results in progressively faster speech with every epoch" and running into my own limitations trying to finetune on Colab Free T4 with 15 GB VRAM, I decided to create a new repo with the following improvements:

1. Uses the most solid codebase with all the key fixes and improvements:
- Base from vspeech/Qwen3-TTS-Train.
- Includes fix by sleepbro: https://github.com/QwenLM/Qwen3-TTS/issues/179#issuecomment-4108009116.
- Includes fix by CamellIyquitous: https://github.com/QwenLM/Qwen3-TTS/issues/179#issuecomment-4132512551.
- Fixed the error where the log folder was not specified.
- Disabled forcing flash_attention_2 only, now it falls back to auto for better GPU compatibility.

2. Reduced VRAM usage:
- Added batch_size argument to prepare_data and lowered the default to 2.
- Switched optimizer to quantized AdamW to significantly cut memory usage.
- Disabled cache and enabled gradient checkpointing to further reduce peak VRAM.

The goal was simple: make it actually usable on free Colab without hacks, crashes, or constant OOM errors.

## Guides
1. For general Qwen TTS information, see the official Qwen3-TTS repository:  
   https://github.com/QwenLM/Qwen3-TTS
2. For finetuning help specific to this setup, see the finetuning section:  
   https://github.com/grimavatar/Qwen3-TTS/tree/main/finetuning

## Acknowledgement
Huge thanks to the original authors and contributors who made this possible.
