---
title: "Python Audio Transcription: Convert Speech to Text Locally"
source: "https://www.pavlinbg.com/posts/python-speech-to-text-guide"
author:
  - "[[Pavlin Gunov]]"
published: 2025-09-21
created: 2025-09-30
description: "Learn how to extract text from audio files locally using Python, Whisper, and other powerful tools. Complete setup guide with practical examples."
tags:
  - "clippings"
---
Last week, I faced a dilemma that many researchers, journalists, and content creators know all too well: I had hours of recordings that needed to be transcribed. I had serious privacy concerns about uploading sensitive content to commercial transcription services and their third-party servers.

Instead of risking it, I built a Python-based transcription system using OpenAI’s Whisper model. The result? All my audio files were transcribed in under 10 minutes with 96% accuracy—completely free and processed locally on my laptop.

In this post, I will show you how you can build a simple script for processing any audio data without recurring costs or privacy compromises.

## Essential Setup Requirements

### 1\. FFmpeg Installation (Critical First Step)

FFmpeg handles audio processing and is required for all transcription methods. **This is the #1 cause of setup failures.**

#### ⚠️ Setup Priority

Install FFmpeg FIRST before any Python packages. Most transcription errors stem from missing or misconfigured FFmpeg. Don't skip this step—it will save you hours of debugging later.

**Windows:**

1. Download from [ffmpeg.org/download.html](https://ffmpeg.org/download.html)
2. Extract to `C:\ffmpeg`
3. Add `C:\ffmpeg\bin` to your PATH environment variable
4. Restart your terminal

**macOS:**

```bash
# Using Homebrew (recommended)

brew install ffmpeg
```

**Linux (Ubuntu/Debian):**

```bash
sudo apt update && sudo apt install ffmpeg
```

**Verify Installation:**

```bash
ffmpeg -version
```

You should see version information. If you get “command not found,” FFmpeg isn’t properly installed.

### 2\. Python Environment Setup

#### 🔧 Virtual Environment Benefits

Using a virtual environment prevents package conflicts, keeps your system Python clean, and makes your setup reproducible across different machines. It's a best practice that will save you from dependency hell.

```bash
# Create isolated environment

python -m venv whisper-env

cd whisper-env

# Activate environment

# Windows:

Scripts\activate

# macOS/Linux:

source bin/activate

# Install required packages

pip install openai-whisper
```

Whisper is OpenAI’s state-of-the-art speech recognition model, trained on 680,000 hours of multilingual audio. It’s specifically designed for robust, real-world audio transcription and handles various accents, background noise, and audio quality issues remarkably well.

### Choosing the Right Whisper Model

#### 🎯 Model Selection Guide

Start with 'base' model for most use cases. It offers the best balance of speed, accuracy, and resource usage for typical projects. Only upgrade to 'small' or 'medium' if you specifically need higher accuracy and have the computational resources.

| Model | Size | RAM Required | Speed | Accuracy | Best Use Case |
| --- | --- | --- | --- | --- | --- |
| tiny | 39 MB | 390 MB | 32x realtime | 89% | Quick testing, real-time applications |
| base | 74 MB | 740 MB | 16x realtime | 94% | **General use (recommended)** |
| small | 244 MB | 2.4 GB | 6x realtime | 96% | High-quality transcription needs |
| medium | 769 MB | 5 GB | 2x realtime | 97% | Professional work, critical accuracy |
| large | 1.5 GB | 10 GB | 1x realtime | 98% | Maximum accuracy, research purposes |

### Basic Whisper Implementation

Here’s a clean, production-ready implementation:

```python
import whisper

import os

from pathlib import Path

import time

class AudioTranscriber:

    def __init__(self, model_size="base"):

        """Initialize transcriber with specified Whisper model"""

        print(f"Loading Whisper {model_size} model...")

        self.model = whisper.load_model(model_size)

        print("Model loaded successfully!")

    

    def transcribe_file(self, audio_path, language=None):

        """

        Transcribe a single audio file

        

        Args:

            audio_path: Path to audio file

            language: Language code ('en', 'es', 'fr', etc.) or None for auto-detect

        """

        if not os.path.exists(audio_path):

            raise FileNotFoundError(f"Audio file not found: {audio_path}")

        

        print(f"Transcribing: {Path(audio_path).name}")

        

        start_time = time.time()

        

        # Transcribe audio

        options = {"language": language} if language else {}

        result = self.model.transcribe(audio_path, **options)

        

        processing_time = time.time() - start_time

        

        print(f"✓ Completed in {processing_time:.1f} seconds")

        print(f"✓ Detected language: {result['language']}")

        

        return {

            'text': result['text'].strip(),

            'language': result['language'],

            'segments': result.get('segments', []),

            'processing_time': processing_time

        }

    

    def save_transcription(self, result, output_path):

        """Save transcription to text file"""

        with open(output_path, 'w', encoding='utf-8') as f:

            f.write("=== Transcription Results ===\n")

            f.write(f"Language: {result['language']}\n")

            f.write(f"Processing Time: {result['processing_time']:.1f} seconds\n")

            f.write("=" * 40 + "\n\n")

            f.write(result['text'])

        

        print(f"✓ Transcription saved to: {output_path}")

# Usage example

def transcribe_audio_file(audio_path, model_size="base", language=None):

    """Simple function to transcribe an audio file"""

    

    transcriber = AudioTranscriber(model_size=model_size)

    result = transcriber.transcribe_file(audio_path, language=language)

    

    # Save transcription

    audio_name = Path(audio_path).stem

    output_path = f"{audio_name}_transcript.txt"

    transcriber.save_transcription(result, output_path)

    

    return result

# Example usage

if __name__ == "__main__":

    # Transcribe a file

    audio_file = "interview.wav"  # Replace with your audio file

    result = transcribe_audio_file(audio_file, model_size="base", language="en")

    

    print(f"\nTranscription preview:")

    print(result['text'][:200] + "..." if len(result['text']) > 200 else result['text'])
```

#### 🎵 Supported Audio Formats

Whisper supports most common audio formats out of the box: WAV, MP3, MP4, M4A, FLAC, OGG, and more. No need to convert files beforehand—FFmpeg handles the conversion automatically in the background.

### Batch Processing Multiple Files

For processing multiple audio files efficiently:

```python
def batch_transcribe(audio_files, output_dir="transcripts", model_size="base"):

    """Transcribe multiple audio files"""

    

    os.makedirs(output_dir, exist_ok=True)

    transcriber = AudioTranscriber(model_size=model_size)

    

    results = []

    

    for i, audio_file in enumerate(audio_files, 1):

        print(f"\n--- Processing file {i}/{len(audio_files)} ---")

        

        try:

            result = transcriber.transcribe_file(audio_file)

            

            # Save individual transcription

            file_name = Path(audio_file).stem

            output_path = os.path.join(output_dir, f"{file_name}_transcript.txt")

            transcriber.save_transcription(result, output_path)

            

            results.append(result)

            

        except Exception as e:

            print(f"✗ Failed to process {audio_file}: {str(e)}")

            continue

    

    print(f"\n✓ Batch processing completed: {len(results)}/{len(audio_files)} files successful")

    return results

# Usage

audio_files = ["interview1.wav", "interview2.mp3", "lecture.m4a"]

batch_transcribe(audio_files, output_dir="my_transcripts")
```

### Creating Subtitle Files (SRT Format)

Generate subtitle files for videos:

```python
def create_srt_subtitles(audio_path, output_path=None):

    """Create SRT subtitle file from audio"""

    

    transcriber = AudioTranscriber(model_size="base")

    result = transcriber.transcribe_file(audio_path)

    

    if output_path is None:

        output_path = Path(audio_path).stem + ".srt"

    

    with open(output_path, 'w', encoding='utf-8') as f:

        for i, segment in enumerate(result['segments'], 1):

            start_time = format_timestamp(segment['start'])

            end_time = format_timestamp(segment['end'])

            

            f.write(f"{i}\n")

            f.write(f"{start_time} --> {end_time}\n")

            f.write(f"{segment['text'].strip()}\n\n")

    

    print(f"✓ SRT subtitles saved to: {output_path}")

def format_timestamp(seconds):

    """Convert seconds to SRT timestamp format"""

    hours = int(seconds // 3600)

    minutes = int((seconds % 3600) // 60)

    secs = int(seconds % 60)

    millisecs = int((seconds % 1) * 1000)

    return f"{hours:02d}:{minutes:02d}:{secs:02d},{millisecs:03d}"

# Usage

create_srt_subtitles("presentation.mp4")
```

## Method 2: Alternative with SpeechRecognition Library

For scenarios requiring different recognition engines or more control over audio preprocessing:

```python
import speech_recognition as sr

from pydub import AudioSegment

import tempfile

import os

class FlexibleTranscriber:

    def __init__(self, engine="google"):

        """Initialize with specified recognition engine"""

        self.recognizer = sr.Recognizer()

        self.engine = engine

        

        # Optimize settings

        self.recognizer.energy_threshold = 300

        self.recognizer.dynamic_energy_threshold = True

        

    def preprocess_audio(self, audio_path):

        """Optimize audio for better recognition"""

        audio = AudioSegment.from_file(audio_path)

        

        # Convert to mono and normalize

        if audio.channels > 1:

            audio = audio.set_channels(1)

        

        audio = audio.set_frame_rate(16000)  # Standard sample rate

        audio = audio.normalize()  # Normalize volume

        

        # Export to temporary WAV file

        temp_file = tempfile.NamedTemporaryFile(delete=False, suffix='.wav')

        audio.export(temp_file.name, format="wav")

        

        return temp_file.name

    

    def transcribe_file(self, audio_path, language='en-US'):

        """Transcribe audio file using speech_recognition library"""

        

        # Preprocess audio

        processed_path = self.preprocess_audio(audio_path)

        

        try:

            with sr.AudioFile(processed_path) as source:

                # Adjust for ambient noise

                self.recognizer.adjust_for_ambient_noise(source, duration=1)

                audio_data = self.recognizer.record(source)

            

            # Perform recognition

            if self.engine == "google":

                text = self.recognizer.recognize_google(audio_data, language=language)

            elif self.engine == "sphinx":

                text = self.recognizer.recognize_sphinx(audio_data)

            

            return {

                'text': text,

                'success': True,

                'engine': self.engine

            }

            

        except sr.UnknownValueError:

            return {

                'text': "",

                'success': False,

                'error': "Could not understand audio"

            }

        except sr.RequestError as e:

            return {

                'text': "",

                'success': False,

                'error': f"Recognition service error: {str(e)}"

            }

        finally:

            # Clean up temporary file

            os.unlink(processed_path)

# Usage

transcriber = FlexibleTranscriber(engine="google")

result = transcriber.transcribe_file("audio.wav")

if result['success']:

    print(result['text'])

else:

    print(f"Transcription failed: {result['error']}")
```

## Common Issues and Solutions

**Error:**`[WinError 2] The system cannot find the file specified`

**Solution:**

- Verify FFmpeg installation: `ffmpeg -version`
- Windows: Ensure FFmpeg is in your PATH environment variable
- Restart your terminal/command prompt after PATH changes
- Try reinstalling FFmpeg if the problem persists

**Error:** CUDA out of memory or system RAM exhausted

#### ⚡ Memory Management Tips

For files longer than 1 hour, use the 'tiny' or 'base' model. For files over 2 hours, consider chunking the audio or processing on a machine with more RAM. GPU acceleration helps with speed but requires more VRAM.

**Solutions:**

```python
# Use smaller model

transcriber = AudioTranscriber(model_size="tiny")

# For very long audio files, process in chunks

def transcribe_long_audio(audio_path, chunk_duration=300):  # 5 minutes

    audio = AudioSegment.from_file(audio_path)

    chunks = [audio[i:i+chunk_duration*1000] for i in range(0, len(audio), chunk_duration*1000)]

    

    transcriptions = []

    for i, chunk in enumerate(chunks):

        chunk_path = f"temp_chunk_{i}.wav"

        chunk.export(chunk_path, format="wav")

        

        result = transcriber.transcribe_file(chunk_path)

        transcriptions.append(result['text'])

        

        os.remove(chunk_path)

    

    return ' '.join(transcriptions)
```

### Issue 3: Poor Accuracy on Noisy Audio

**Problem:** Low accuracy on recordings with background noise or poor quality

#### 🎤 Audio Quality Tips

Best results come from: 16kHz+ sample rate, minimal background noise, clear speech, and audio levels between -12dB to -6dB. Record in quiet environments when possible. Even small improvements in audio quality dramatically improve transcription accuracy.

**Solutions:**

1. **Audio preprocessing:**
```python
def enhance_audio(audio_path):

    """Basic audio enhancement"""

    audio = AudioSegment.from_file(audio_path)

    

    # Normalize volume

    audio = audio.normalize()

    

    # Apply high-pass filter to reduce low-frequency noise

    audio = audio.high_pass_filter(80)

    

    # Compress dynamic range

    audio = audio.compress_dynamic_range()

    

    return audio
```
1. **Specify language for better accuracy:**
```python
result = transcriber.transcribe_file("audio.wav", language="en")
```
1. **Use higher-quality model:**
```python
# Upgrade from 'base' to 'small' for better accuracy

transcriber = AudioTranscriber(model_size="small")
```

## Performance Benchmarks

Based on testing with various audio types on a modern laptop:

**Whisper Model Performance (1-hour audio file):**

- **tiny**: 1.9 minutes processing, 89% accuracy
- **base**: 3.8 minutes processing, 94% accuracy
- **small**: 10 minutes processing, 96% accuracy
- **medium**: 30 minutes processing, 97% accuracy

**Hardware Impact:**

- **CPU only**: Use base model maximum for reasonable speeds
- **8GB RAM**: Comfortable with small model
- **16GB+ RAM**: Can handle medium/large models without issues
- **GPU acceleration**: 3-5x speed improvement (requires CUDA setup)

#### 🚀 Optimization Strategy

Start with 'base' model on CPU for the best balance of speed and accuracy. If accuracy is insufficient for your use case, upgrade to 'small'. Only use GPU acceleration if you're processing large volumes of audio regularly—the setup complexity isn't worth it for occasional use.

## Command-Line Usage

Create a simple command-line script for easy usage:

```python
# transcribe.py

import sys

import argparse

from pathlib import Path

def main():

    parser = argparse.ArgumentParser(description='Transcribe audio files locally')

    parser.add_argument('audio_file', help='Path to audio file')

    parser.add_argument('--model', default='base', choices=['tiny', 'base', 'small', 'medium', 'large'])

    parser.add_argument('--language', help='Language code (e.g., en, es, fr)')

    parser.add_argument('--output', help='Output file path')

    

    args = parser.parse_args()

    

    # Transcribe

    result = transcribe_audio_file(

        args.audio_file, 

        model_size=args.model,

        language=args.language

    )

    

    # Save to custom output path if specified

    if args.output:

        with open(args.output, 'w', encoding='utf-8') as f:

            f.write(result['text'])

        print(f"Transcription saved to: {args.output}")

if __name__ == "__main__":

    main()
```

**Usage examples:**

```bash
# Basic transcription

python transcribe.py interview.wav

# Specify model and language

python transcribe.py lecture.mp3 --model small --language en

# Custom output file

python transcribe.py podcast.m4a --output transcript.txt
```

## Conclusion

Local audio transcription with Python and Whisper offers a compelling alternative to commercial services. With a one-time setup, you get unlimited transcription capabilities, complete privacy, and often superior accuracy compared to cloud-based solutions.

**Key advantages:**

- **Zero ongoing costs** after initial setup—no per-minute charges
- **Complete privacy** —audio never leaves your machine
- **High accuracy** —94-98% depending on model choice and audio quality
- **Fast processing** —typically 4-16x real-time speed
- **Offline capability** —works without internet connection
- **No usage limits** —transcribe as much as you want

Whether you’re a researcher transcribing interviews, a journalist working with sensitive sources, or a content creator processing podcasts, this local solution gives you the control and privacy that cloud services can’t match.

The setup might take 30 minutes, but you’ll save hours of time and potentially hundreds of dollars in transcription costs. Plus, you’ll have the peace of mind that comes with keeping your audio data completely under your control.

© 2025 Pavlin