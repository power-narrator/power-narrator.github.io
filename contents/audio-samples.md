{% set title="Audio Samples (Internal)" %}
<frontmatter>
  title: {{ title }}
  pageNav: 3
</frontmatter>

<br>

# {{ title }}


{% macro embed_audio(filename) %} <audio controls><source src="{{ baseUrl }}/audio-samples/{{ filename }}" type="audio/mpeg"></audio> {% endmacro %}


## Pronunciation and articulation

Model | Sample | Explanation
------|--------|------------
Chirp | {{ embed_audio("01-pronunciation-chirp-3-hd.mp3") }} | "S" in "staging area" was dragged
Gemini | {{ embed_audio("01-pronunciation-gemini-3.1-flash-tts-preview.mp3") }} | Proper articulation

---

## Pitch and stress

Model | Sample | Explanation
------|--------|------------
Chirp | {{ embed_audio("02-pitch-range-chirp-3-hd.mp3") }} | The rhetorical question has a limited pitch range.
Gemini | {{ embed_audio("02-pitch-range-gemini-3.1-flash-tts-preview.mp3") }} | A wider pitch range, especially when listing the options in the rhetorical question.

Model | Sample | Explanation
------|--------|------------
Chirp | {{ embed_audio("03-capitals-plain-chirp-3-hd.mp3") }} | Without capitalization, "this" was not stressed.
Chirp | {{ embed_audio("03-capitals-uppercase-chirp-3-hd.mp3") }} | With "THIS" capitalized, some stress was placed on it with an upward pitch.
Gemini | {{ embed_audio("03-capitals-plain-gemini-3.1-flash-tts-preview.mp3") }} | Without capitalization, "this" had some stress with an upward pitch.
Gemini | {{ embed_audio("03-capitals-uppercase-gemini-3.1-flash-tts-preview.mp3") }} | With "THIS" capitalized, the upward pitch was even greater.

---

## Rhythm, phrasing and pausing

Model | Sample | Explanation
------|--------|------------
Chirp | {{ embed_audio("04-pause-length-chirp-3-hd.mp3") }} | Pauses had similar lengths across punctuation marks, and sentences generally had the same rhythm.
Gemini | {{ embed_audio("04-pause-length-gemini-3.1-flash-tts-preview.mp3") }} | Pause lengths varied even for the same punctuation. Statements were sometimes faster, while other sentences slowed down to show uncertainty.

---

Model | Sample | Explanation
------|--------|------------
Chirp | {{ embed_audio("05-unexpected-pause-chirp-3-hd.mp3") }} | An unexpected pause in "that I'd", where there is no punctuation.
Gemini | {{ embed_audio("05-unexpected-pause-gemini-3.1-flash-tts-preview.mp3") }} | No unexpected pause.

---

## Continuity across sections

Model | Sample | Explanation
------|--------|------------
Chirp | {{ embed_audio("06-section-joins-chirp-3-hd.mp3") }} | Some pauses between sections are very short, making consecutive sentences sound like one. Examples include "empty remote repo. In Git, this" and "usually a URL. You also give".
Gemini | {{ embed_audio("06-section-joins-gemini-3.1-flash-tts-preview.mp3") }} | Transitions between sections are more natural.

---

## Expressiveness and appropriateness

Model | Sample | Explanation
------|--------|------------
Gemini | {{ embed_audio("07-tone-no-prompt-gemini-3.1-flash-tts-preview.mp3") }} | No prompt.
Gemini | {{ embed_audio("07-tone-excited-gemini-3.1-flash-tts-preview.mp3") }} | Prompt: Say this excitedly.
Gemini | {{ embed_audio("07-tone-lethargic-gemini-3.1-flash-tts-preview.mp3") }} | Prompt: Say this lethargically.

---

## Acoustic quality and voice consistency

Model | Sample | Explanation
------|--------|------------
Gemini 2.5 Pro TTS | {{ embed_audio("08-accent-take1-indian-gemini-2.5-pro-tts.mp3") }} | A generation with an Indian accent.
Gemini 2.5 Pro TTS | {{ embed_audio("08-accent-take2-american-gemini-2.5-pro-tts.mp3") }} | Another generation with the expected American accent, with no change to the generation parameters.

---

## Controllability and instruction adherence

Model | Sample | Explanation
------|--------|------------
Gemini | {{ embed_audio("09-prompt-capitals-off-gemini-3.1-flash-tts-preview.mp3") }} | No prompt.
Gemini | {{ embed_audio("09-prompt-capitals-on-gemini-3.1-flash-tts-preview.mp3") }} | Prompt: emphasise all words with all letters capitalised. Words: DEEPER, THIS.
Gemini | {{ embed_audio("10-prompt-quotes-off-gemini-3.1-flash-tts-preview.mp3") }} | No prompt.
Gemini | {{ embed_audio("10-prompt-quotes-on-gemini-3.1-flash-tts-preview.mp3") }} | Prompt: say the part in quotes slowly. Part in quotes: "pull from upstream, push to the fork".

---

Model | Sample | Explanation
------|--------|------------
Gemini | {{ embed_audio("11-markup-tags-off-gemini-3.1-flash-tts-preview.mp3") }} | No tags used.
Gemini | {{ embed_audio("11-markup-tags-on-gemini-3.1-flash-tts-preview.mp3") }} | Text: [excitedly] In our example, [long pause] if we stage the banks file, [very long pause] this is what happens. [clear throat]

---
