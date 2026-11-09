# Global Quran Data Repository

This repository is setup to easily manage Global Quran text data with repository, which is linked with GQ backend. 

Anything added here, will be pushed to Global Quran api instantly with any changes made. 


Adding New File
---------------

If you are adding new file, please use language code with concatinated (.) with author name in lower case. 
 
File must have

- filename should end with .txt file
- each line is each ayah, there are 6236 ayahs
- after 6237 lines, You must add Quran parameters, which system reads to understand what file is about. check example of Quran parameters below.


Quran Parameters
----------------

Following is Quran parameters, which should be written inside .txt file after 6237 lines.

| Name | Requried | Description |
|---|---|---|
| ID | Yes  | quran id to use, it should start with language code and concatinated with period (.) then name of translator without any space  |
| Language | Yes | lanuage is it in |
| Name | Yes | English name of the translator |
| Translator | Yes | Name in native language  |
| Source | Yes | Source for this data, if its from different website, then just give domain.com |
| Type   | No  | default value is `translation`, Values are `translation` or `quran` - changing this wont update value in backend |
| version | No | Which version of our application supports this data, sometime it needs special function to parse it, which needs to be added in functionality |
| default | No | value of `Yes` or `No`, If one language has more then 1 data set, then this value can come useful for selection which one should be default selction for user |
| status  | No | default value is `active`, This can have `active`, `blocked`,`incomplete` and `draft` |


Following is the example on how it should look like in the end of the data file

```
...

#=====================================================================
#
#  Quran Translation
#  Name: Arberry
#  Translator: A. J. Arberry
#  Language: English
#  ID: en.arberry
#  Last Update: March 3, 2011
#  Source: Tanzil.net
#
#=====================================================================

```




Audio
-----

The audio files themselves live in the audio bucket (`audio.globalquran.com`), not here. This folder holds **one small YAML file per reciter** (`Audio/<id>.yml`, id like `ar.alafasy` = language code + reciter, lower case) that describes it and lists every variant that exists. Pushing a change creates or updates the reciter in the database. `#` comments are allowed and ignored.

```yaml
id: ar.alafasy                  # must match the file name
name: Mishary Alafasy           # English name
native_name: مشاري العفاسي       # optional
language: Arabic                # for people; the language code is the start of the id
description: Kuwaiti reciter... # optional, free text: a short profile of the reciter (who they are, their history)
origin: Kuwait                  # optional: where the reciter is from
wikipedia: https://en.wikipedia.org/wiki/Mishary_Rashid_Alafasy   # optional: link to their Wikipedia page (no photos are stored)
status: draft                   # only used when the reciter is new: draft | active | incomplete | blocked (the admin changes it afterwards)
default: no                     # only used when new
variants:                       # one entry per format / bitrate / mode that exists
  - format: mp3                 # mp3 | ogg
    kbs: 128
    mode: versebyverse          # versebyverse (default) | surahbysurah | juzbyjuz
    status: active              # only used when this variant is new
    source: VerseByVerseQuran.com        # optional: where the files came from
    source_url: https://example.com/...  # optional
    audhubillah: yes            # verse files: file 0 (a'udhu billah) exists
    path: ar.alafasy/mp3/128kbs/         # optional: folder in the bucket (default below)
    timing:                     # optional, reserved for ayah/word timestamps (not processed yet)
      ayah: ar.alafasy/timing/ayah/
      word: ar.alafasy/timing/word/
```

Where the files are in the bucket (default `path`):

| mode | folder | file names |
|---|---|---|
| `versebyverse` | `<id>/<format>/<kbs>kbs/` | `0` (a'udhu billah) and `1`..`6236` (global verse number), e.g. `1.mp3` |
| `surahbysurah` | `<id>/<format>/<kbs>kbs/surah/` | `1`..`114` |
| `juzbyjuz` | `<id>/<format>/<kbs>kbs/juz/` | `1`..`30` |

`source_url` is only a record of where the files came from. When files are copied into the bucket they are always renamed to the structure above, whatever the source calls them (everyayah.com `<surah><ayah>.mp3` and cdn.islamic.network `<verse number>.mp3` are supported).

The same reciter can have any number of variants (several formats, bitrates, and verse-by-verse together with surah-by-surah). Removing a variant from the file blocks it in the database; the admin decides what is live.
