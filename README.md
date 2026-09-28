What AgentNode is

AgentNode is a macOS menubar app for voice-typing code. Hold Right Option (⌥), speak, and let go. Your words are typed wherever your cursor is, with developer terms spelled correctly. You get kubectl and OAuth2PasswordBearer instead of "cube control" and "o auth two password bearer."

The idea: general speech-to-text will never learn your vocabulary. A small correction layer can fix the transcript afterward if it knows your tools, your code's names and what's on your screen.

How it works:

Transcription: Whisper small.en runs on your Mac through mlx-whisper, so audio never leaves the machine and is never saved.
Correction: a lexicon built from your code's names fixes the jargon. It matches by sound and by spelling, and it narrows the word list to the file you have open, which it reads from the front window's title.
Built-in safeguard: it leaves ordinary English alone, so "pseudo code" stays as written but "pseudo apt update" becomes sudo apt update.
Learns your code automatically: it reads the workspaces you have open in Cursor and learns their function and class names. You can also add folders with Add code folder….

App features: a floating pill that shows when it's listening or transcribing, a setup window for the Microphone and Accessibility permissions, a menu with your last five transcripts, and a --selftest check.

Results (from core/RESULTS.md, measured on simulated Whisper errors):

86% of jargon terms corrected
Word error rate cut from 27.8% to 4.1%
No wrong changes to plain English
Under 1 ms median per correction

Status:

It's built with Python and rumps and packaged as a signed AgentNode.app (about 490 MB) plus a DMG (about 193 MB).
It runs on Apple silicon only.
It isn't notarized yet because that needs a $99/yr Apple Developer ID. Until then, people who download it have to right-click → Open the first time.
From my notes (last updated July 15, so possibly out of date): two small code fixes are still waiting for the next build. One is adding multiprocessing.freeze_support(); the other is removing leftover debug trace lines.

Repo layout:

apps/menubar/: the app
core/agentnode_core/: the correction engine and its test harness
packaging/: build, DMG and notarization scripts
docs/: landing page and planning docs
