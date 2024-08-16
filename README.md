# Cog Whisper Diarization

Audio transcribing + diarization pipeline.

## Models used

- Whisper Large v3 (CTranslate 2 version `faster-whisper==1.0.3`)
- Pyannote audio 3.3.1

## Installation (without cog)

```
sudo apt install ffmpeg libmagic1
```
```
git clone https://github.com/d8rt8v/whisper-diarization.git
cd whisper-diarization
python3 -m venv env
source env/bin/activate
pip install -r requirements.txt
```
## Usage

Run app.py 
```
python app.py
```

### Input

- `file_string: str`: Either provide a Base64 encoded audio file.
- `file_url: str`: Or provide a direct audio file URL.
- `file: Path`: Or provide an audio file.
- `group_segments: bool`: Group segments of the same speaker shorter than 2 seconds apart. Default is `True`.
- `num_speakers: int`: Number of speakers. Leave empty to autodetect. Must be between 1 and 50.
- `translate: bool`: Translate the speech into English.
- `language: str`: Language of the spoken words as a language code like 'en'. Leave empty to auto detect language.
- `prompt: str`: Vocabulary: provide names, acronyms, and loanwords in a list. Use punctuation for best accuracy. Also now used as 'hotwords' paramater in transcribing,
- `offset_seconds: int`: Offset in seconds, used for chunked inputs. Default is 0.
- `transcript_output_format: str`: Specify the format of the transcript output: individual words with timestamps, full text of segments, or a combination of both.
  - Default is `both`.
  - Options are `words_only`, `segments_only`, `both`,

### Output

- `segments: List[Dict]`: List of segments with speaker, start and end time.
  - Includes `avg_logprob` for each segment and `probability` for each word level segment.
- `num_speakers: int`: Number of speakers (detected, unless specified in input).
- `language: str`: Language of the spoken words as a language code like 'en' (detected, unless specified in input).

## Thanks to

- [pyannote](https://github.com/pyannote/pyannote-audio)
- [faster-whisper](https://github.com/SYSTRAN/faster-whisper)
- [whisper](https://github.com/openai/whisper)
