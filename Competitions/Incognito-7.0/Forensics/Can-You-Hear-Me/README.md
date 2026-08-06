# Can You Hear Me?

## Competition
Incognito 7.0

## Category
Forensics

## Difficulty
Hard

## Challenge Description

*Challenge description not provided.*

## Tools Used

- Terminal utilities (File analysis)
- `ffmpeg`
- `sox`
- Spectrogram Analysis Tool

## Investigation

### Step 1 - Initial Analysis

Starting off, the first move was checking what kind of file had been handed over to ensure it wasn’t disguised under a false name. Using basic terminal tools, a close look at the file’s actual structure took place, stripping away any surface-level confusion about its real identity. Following this, provided clues were studied one by one to narrow down possible hiding spots for data, cutting out random guesses. To maintain absolute certainty before proceeding with advanced manipulation, I performed a secondary, more granular file type and metadata analysis to verify the exact encoding parameters and structural headers. 

### Step 2 - Discovery

With every structural detail locked in place, the next step unfolded through a detailed `ffmpeg` sequence aimed at rendering the entire audio pathway. Because precision mattered most, this method pulled out all sound elements without compression—leaving nothing behind. Hidden layers, extra tracks, and tucked-away metadata all stayed visible, avoiding gaps that might have slipped past earlier scans.

### Step 3 - Extraction

Midway through the review, signs pointed to hidden patterns in high-frequency segments. Using `sox`, a narrow slice of sound came into focus. I applied a targeted bandpass filter set between 15,000 Hz and 18,000 Hz, fading out surrounding noise. What remained was exactly the range where encoded signals often hide, cleanly removing the dominant lower tones.

Later, the cleaned signal appeared as a spectrogram, turning sharp audio pulses into visible patterns across time.

## Solution

Looking closely at the spectrogram revealed a clear structure: vertical segments appeared one after another, separated and precise. Within every segment, six frequency zones stood out, their layout intentional. A bright signal either showed up or did not in each zone, matching perfectly to binary (on/off) values. That setup meant each section carried precisely six units of hidden information (6-bit). The pattern repeated consistently across all divisions.

Starting from the highest frequency row, I moved step by step through each layer of patterns, noting the on-off values in order. Because every segment held six digits, grouping them that way made decoding straightforward. After lining up those sets, I translated each cluster into a character, slowly forming parts of a larger sequence. When all pieces came together correctly, the structure matched what was expected and revealed the flag.

## Flag
IIITL{st3r30_5p3c7r0g4r4m_h1dd3n}

## Lessons Learned

- **Audio Forensics:** Successfully isolated high-frequency data using bandpass filtering (`sox`) and uncovered hidden data by analyzing binary patterns mapped to frequency zones within a spectrogram.
- **Methodology:** Emphasized the importance of thorough initial file and metadata verification to prevent wasted effort later in the analysis pipeline.