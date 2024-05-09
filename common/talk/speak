#!/bin/bash

# Usage:
#  speak <voice_id> <textfile>

function installed() { command -v $1 >/dev/null 2>&1; }

if installed espeak; then
  espeak -v en-us+m$1 -s 225 -p 50 -a 200 -g 5 -k 5 -f $2

elif installed piper && installed aplay; then
  cat $2 | piper --model ~/en_US-lessac-medium.onnx --output-raw | aplay -q -r 22050 -f S16_LE -t raw -

# for Mac
elif installed say; then
  say -f $2

else
  echo 'Install espeak ("brew install espeak" or "apt-get install espeak"),'
  echo 'piper ("pip install piper-tts" or https://github.com/rhasspy/piper) with aplay,'
  echo 'or elevenlabs ("pip install elevenlabs") with ffplay.'
  echo '(export ELEVEN_API_KEY if you have an api key from https://beta.elevenlabs.io)'
fi
