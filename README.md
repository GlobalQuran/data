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
| Origin | No | Country or place the translator is from, e.g. `Pakistan` |
| Wikipedia | No | Wikipedia page about the translator, must look like `https://en.wikipedia.org/wiki/Name` (only add a page you have checked is the right person) |
| Profile | No | One or two lines about the translator, on one line |


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

<!-- LISTS:START (generated by tools/update_readme_lists.py, do not edit by hand) -->

### Available data

Everything here is served from the CDN. Per edition: the whole Quran as one JSON file `https://cdn.globalquran.com/quran_data/complete/json/<id>.json`, one verse `https://cdn.globalquran.com/quran_data/verse/<id>/<verse number 1..6236>.txt`, one surah `https://cdn.globalquran.com/quran_data/surah/<id>/<1..114>.txt`, page `…/page/<id>/<1..604>.txt` and juz `…/juz/<id>/<1..30>.txt` (each also as `.jsonp`). Editions marked _(draft)_ or _(incomplete)_ are not public yet, so their links may not work until they are enabled.

#### Quran texts (12)

Arabic text editions.

| ID (source file) | Name | Language | Translator / author | Read it (CDN) |
|---|---|---|---|---|
| [`quran-buck`](Quran/quran-buck.txt) | Buck _(pending)_ | Arabic | Buck | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-buck.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-buck/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-buck/1.txt) |
| [`quran-corpus-qd`](Quran/quran-corpus-qd.txt) | Corpus _(pending)_ | Arabic | Corpus | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-corpus-qd.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-corpus-qd/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-corpus-qd/1.txt) |
| [`quran-kids`](Quran/quran-kids.txt) | Kids | Arabic | Kids | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-kids.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-kids/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-kids/1.txt) |
| [`quran-simple-clean`](Quran/quran-simple-clean.txt) | Simple Clean | Arabic | Simple Clean | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-simple-clean.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-simple-clean/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-simple-clean/1.txt) |
| [`quran-simple-enhanced`](Quran/quran-simple-enhanced.txt) | Simple Enhanced | Arabic | Simple Enhanced | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-simple-enhanced.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-simple-enhanced/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-simple-enhanced/1.txt) |
| [`quran-simple-min`](Quran/quran-simple-min.txt) | Simple Minimal | Arabic | Simple Minimal | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-simple-min.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-simple-min/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-simple-min/1.txt) |
| [`quran-simple`](Quran/quran-simple.txt) | Simple | Arabic | Simple | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-simple.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-simple/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-simple/1.txt) |
| [`quran-tajweed`](Quran/quran-tajweed.txt) | Tajweed | Arabic | Tajweed | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-tajweed.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-tajweed/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-tajweed/1.txt) |
| [`quran-uthmani-hafs`](Quran/quran-uthmani-hafs.txt) | Uthamani Hafs | Arabic | Uthamani Hafs | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-uthmani-hafs.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-uthmani-hafs/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-uthmani-hafs/1.txt) |
| [`quran-uthmani-min`](Quran/quran-uthmani-min.txt) | Uthmani Minimal | Arabic | Uthmani Minimal | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-uthmani-min.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-uthmani-min/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-uthmani-min/1.txt) |
| [`quran-uthmani`](Quran/quran-uthmani.txt) | Uthamani | Arabic | Uthamani | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-uthmani.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-uthmani/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-uthmani/1.txt) |
| [`quran-wordbyword`](Quran/quran-wordbyword.txt) | Word By Word | Arabic | Word By Word | [JSON](https://cdn.globalquran.com/quran_data/complete/json/quran-wordbyword.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/quran-wordbyword/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/quran-wordbyword/1.txt) |

#### Translations (117)

Translations and tafsir, by language code.

| ID (source file) | Name | Language | Translator / author | Read it (CDN) |
|---|---|---|---|---|
| [`am.sadiq`](translation/am.sadiq.txt) | ሳዲቅ & ሳኒ ሐቢብ _(draft)_ | Amharic | Muhammed Sadiq and Muhammed Sani Habib | [JSON](https://cdn.globalquran.com/quran_data/complete/json/am.sadiq.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/am.sadiq/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/am.sadiq/1.txt) |
| [`ar.jalalayn`](translation/ar.jalalayn.txt) | تفسير الجلالين | Arabic | Jalal ad-Din al-Mahalli and Jalal ad-Din as-Suyuti | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ar.jalalayn.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ar.jalalayn/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ar.jalalayn/1.txt) |
| [`ar.muyassar`](translation/ar.muyassar.txt) | تفسير المیسر | Arabic | King Fahad Quran Complex | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ar.muyassar.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ar.muyassar/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ar.muyassar/1.txt) |
| [`az.mammadaliyev`](translation/az.mammadaliyev.txt) | Məmmədəliyev & Bünyadov | Azerbaijani | Vasim Mammadaliyev and Ziya Bunyadov | [JSON](https://cdn.globalquran.com/quran_data/complete/json/az.mammadaliyev.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/az.mammadaliyev/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/az.mammadaliyev/1.txt) |
| [`az.musayev`](translation/az.musayev.txt) | Musayev | Azerbaijani | Alikhan Musayev | [JSON](https://cdn.globalquran.com/quran_data/complete/json/az.musayev.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/az.musayev/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/az.musayev/1.txt) |
| [`ber.mensur`](translation/ber.mensur.txt) | At Mensur _(draft)_ | Amazigh | Ramdane At Mansour | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ber.mensur.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ber.mensur/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ber.mensur/1.txt) |
| [`bg.theophanov`](translation/bg.theophanov.txt) | Теофанов | Bulgarian | Tzvetan Theophanov | [JSON](https://cdn.globalquran.com/quran_data/complete/json/bg.theophanov.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/bg.theophanov/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/bg.theophanov/1.txt) |
| [`bn.bengali`](translation/bn.bengali.txt) | মুহিউদ্দীন খান | Bengali | Muhiuddin Khan | [JSON](https://cdn.globalquran.com/quran_data/complete/json/bn.bengali.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/bn.bengali/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/bn.bengali/1.txt) |
| [`bn.hoque`](translation/bn.hoque.txt) | জহুরুল হক _(draft)_ | Bengali | Zohurul Hoque | [JSON](https://cdn.globalquran.com/quran_data/complete/json/bn.hoque.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/bn.hoque/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/bn.hoque/1.txt) |
| [`bs.korkut`](translation/bs.korkut.txt) | Korkut | Bosnian | Besim Korkut | [JSON](https://cdn.globalquran.com/quran_data/complete/json/bs.korkut.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/bs.korkut/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/bs.korkut/1.txt) |
| [`bs.mlivo`](translation/bs.mlivo.txt) | Mlivo | Bosnian | Mustafa Mlivo | [JSON](https://cdn.globalquran.com/quran_data/complete/json/bs.mlivo.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/bs.mlivo/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/bs.mlivo/1.txt) |
| [`cs.hrbek`](translation/cs.hrbek.txt) | Hrbek | Czech | Preklad I. Hrbek | [JSON](https://cdn.globalquran.com/quran_data/complete/json/cs.hrbek.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/cs.hrbek/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/cs.hrbek/1.txt) |
| [`cs.nykl`](translation/cs.nykl.txt) | Nykl | Czech | A. R. Nykl | [JSON](https://cdn.globalquran.com/quran_data/complete/json/cs.nykl.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/cs.nykl/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/cs.nykl/1.txt) |
| [`de.aburida`](translation/de.aburida.txt) | Abu Rida | German | Abu Rida Muhammad ibn Ahmad ibn Rassoul | [JSON](https://cdn.globalquran.com/quran_data/complete/json/de.aburida.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/de.aburida/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/de.aburida/1.txt) |
| [`de.bubenheim`](translation/de.bubenheim.txt) | Bubenheim & Elyas | German | A. S. F. Bubenheim and N. Elyas | [JSON](https://cdn.globalquran.com/quran_data/complete/json/de.bubenheim.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/de.bubenheim/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/de.bubenheim/1.txt) |
| [`de.khoury`](translation/de.khoury.txt) | Khoury | German | Adel Theodor Khoury | [JSON](https://cdn.globalquran.com/quran_data/complete/json/de.khoury.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/de.khoury/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/de.khoury/1.txt) |
| [`de.zaidan`](translation/de.zaidan.txt) | Zaidan | German | Amir Zaidan | [JSON](https://cdn.globalquran.com/quran_data/complete/json/de.zaidan.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/de.zaidan/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/de.zaidan/1.txt) |
| [`dv.divehi`](translation/dv.divehi.txt) | ދިވެހި | Divehi | Office of the President of Maldives | [JSON](https://cdn.globalquran.com/quran_data/complete/json/dv.divehi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/dv.divehi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/dv.divehi/1.txt) |
| [`en.ahmedali`](translation/en.ahmedali.txt) | Ahmed Ali | English | Ahmed Ali | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.ahmedali.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.ahmedali/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.ahmedali/1.txt) |
| [`en.ahmedraza`](translation/en.ahmedraza.txt) | Ahmed Raza Khan | English | Ahmed Raza Khan | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.ahmedraza.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.ahmedraza/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.ahmedraza/1.txt) |
| [`en.arberry`](translation/en.arberry.txt) | Arberry | English | A. J. Arberry | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.arberry.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.arberry/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.arberry/1.txt) |
| [`en.asad`](translation/en.asad.txt) | Asad | English | Muhammad Asad | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.asad.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.asad/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.asad/1.txt) |
| [`en.daryabadi`](translation/en.daryabadi.txt) | Daryabadi | English | Abdul Majid Daryabadi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.daryabadi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.daryabadi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.daryabadi/1.txt) |
| [`en.hilali`](translation/en.hilali.txt) | Hilali & Khan | English | Muhammad Taqi-ud-Din al-Hilali and Muhammad Muhsin Khan | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.hilali.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.hilali/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.hilali/1.txt) |
| [`en.itani`](translation/en.itani.txt) | Itani _(draft)_ | English | Talal Itani | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.itani.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.itani/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.itani/1.txt) |
| [`en.maududi`](translation/en.maududi.txt) | Maududi | English | Abul Ala Maududi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.maududi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.maududi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.maududi/1.txt) |
| [`en.mubarakpuri`](translation/en.mubarakpuri.txt) | Mubarakpuri _(draft)_ | English | Safi-ur-Rahman al-Mubarakpuri | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.mubarakpuri.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.mubarakpuri/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.mubarakpuri/1.txt) |
| [`en.pickthall`](translation/en.pickthall.txt) | Pickthall | English | Mohammed Marmaduke William Pickthall | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.pickthall.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.pickthall/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.pickthall/1.txt) |
| [`en.qarai`](translation/en.qarai.txt) | Qarai _(draft)_ | English | Ali Quli Qarai | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.qarai.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.qarai/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.qarai/1.txt) |
| [`en.qaribullah`](translation/en.qaribullah.txt) | Qaribullah & Darwish | English | Hasan al-Fatih Qaribullah and Ahmad Darwish | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.qaribullah.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.qaribullah/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.qaribullah/1.txt) |
| [`en.sahih`](translation/en.sahih.txt) | Saheeh International | English | Saheeh International | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.sahih.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.sahih/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.sahih/1.txt) |
| [`en.sarwar`](translation/en.sarwar.txt) | Sarwar | English | Muhammad Sarwar | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.sarwar.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.sarwar/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.sarwar/1.txt) |
| [`en.shakir`](translation/en.shakir.txt) | Shakir | English | Mohammad Habib Shakir | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.shakir.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.shakir/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.shakir/1.txt) |
| [`en.wahiduddin`](translation/en.wahiduddin.txt) | Wahiduddin Khan _(draft)_ | English | Wahiduddin Khan | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.wahiduddin.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.wahiduddin/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.wahiduddin/1.txt) |
| [`en.yusufali`](translation/en.yusufali.txt) | Yusuf Ali | English | Abdullah Yusuf Ali | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.yusufali.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.yusufali/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.yusufali/1.txt) |
| [`es.asad`](translation/es.asad.txt) | Asad | Spanish | Muhammad Asad - Abdurrasak Pérez | [JSON](https://cdn.globalquran.com/quran_data/complete/json/es.asad.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/es.asad/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/es.asad/1.txt) |
| [`es.bornez`](translation/es.bornez.txt) | Bornez _(draft)_ | Spanish | Raúl González Bórnez | [JSON](https://cdn.globalquran.com/quran_data/complete/json/es.bornez.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/es.bornez/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/es.bornez/1.txt) |
| [`es.cortes`](translation/es.cortes.txt) | Cortes | Spanish | Julio Cortes | [JSON](https://cdn.globalquran.com/quran_data/complete/json/es.cortes.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/es.cortes/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/es.cortes/1.txt) |
| [`es.garcia`](translation/es.garcia.txt) | Garcia _(draft)_ | Spanish | Muhammad Isa García | [JSON](https://cdn.globalquran.com/quran_data/complete/json/es.garcia.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/es.garcia/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/es.garcia/1.txt) |
| [`fa.ansarian`](translation/fa.ansarian.txt) | انصاریان | Persian | Hussain Ansarian | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.ansarian.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.ansarian/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.ansarian/1.txt) |
| [`fa.ayati`](translation/fa.ayati.txt) | آیتی | Persian | AbdolMohammad Ayati | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.ayati.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.ayati/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.ayati/1.txt) |
| [`fa.bahrampour`](translation/fa.bahrampour.txt) | بهرام پور | Persian | Abolfazl Bahrampour | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.bahrampour.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.bahrampour/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.bahrampour/1.txt) |
| [`fa.fooladvand`](translation/fa.fooladvand.txt) | فولادوند | Persian | Mohammad Mahdi Fooladvand | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.fooladvand.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.fooladvand/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.fooladvand/1.txt) |
| [`fa.gharaati`](translation/fa.gharaati.txt) | قرائتی _(draft)_ | Persian | Mohsen Gharaati | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.gharaati.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.gharaati/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.gharaati/1.txt) |
| [`fa.ghomshei`](translation/fa.ghomshei.txt) | الهی قمشه‌ای | Persian | Mahdi Elahi Ghomshei | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.ghomshei.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.ghomshei/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.ghomshei/1.txt) |
| [`fa.khorramdel`](translation/fa.khorramdel.txt) | خرمدل | Persian | Mostafa Khorramdel | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.khorramdel.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.khorramdel/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.khorramdel/1.txt) |
| [`fa.khorramshahi`](translation/fa.khorramshahi.txt) | خرمشاهی | Persian | Baha'oddin Khorramshahi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.khorramshahi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.khorramshahi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.khorramshahi/1.txt) |
| [`fa.makarem`](translation/fa.makarem.txt) | مکارم شیرازی | Persian | Naser Makarem Shirazi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.makarem.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.makarem/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.makarem/1.txt) |
| [`fa.moezzi`](translation/fa.moezzi.txt) | معزی | Persian | Mohammad Kazem Moezzi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.moezzi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.moezzi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.moezzi/1.txt) |
| [`fa.mojtabavi`](translation/fa.mojtabavi.txt) | مجتبوی | Persian | Sayyed Jalaloddin Mojtabavi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.mojtabavi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.mojtabavi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.mojtabavi/1.txt) |
| [`fa.sadeqi`](translation/fa.sadeqi.txt) | صادقی تهرانی _(draft)_ | Persian | Mohammad Sadeqi Tehrani | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.sadeqi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.sadeqi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.sadeqi/1.txt) |
| [`fa.safavi`](translation/fa.safavi.txt) | صفوی _(draft)_ | Persian | Sayyed Mohammad Reza Safavi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fa.safavi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fa.safavi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fa.safavi/1.txt) |
| [`fr.hamidullah`](translation/fr.hamidullah.txt) | Hamidullah | French | Muhammad Hamidullah | [JSON](https://cdn.globalquran.com/quran_data/complete/json/fr.hamidullah.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/fr.hamidullah/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/fr.hamidullah/1.txt) |
| [`ha.gumi`](translation/ha.gumi.txt) | Gumi | Hausa | Abubakar Mahmoud Gumi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ha.gumi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ha.gumi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ha.gumi/1.txt) |
| [`hi.farooq`](translation/hi.farooq.txt) | फ़ारूक़ ख़ान & अहमद | Hindi | Muhammad Farooq Khan and Muhammad Ahmed | [JSON](https://cdn.globalquran.com/quran_data/complete/json/hi.farooq.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/hi.farooq/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/hi.farooq/1.txt) |
| [`hi.hindi`](translation/hi.hindi.txt) | फ़ारूक़ ख़ान & नदवी | Hindi | Suhel Farooq Khan and Saifur Rahman Nadwi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/hi.hindi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/hi.hindi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/hi.hindi/1.txt) |
| [`id.indonesian`](translation/id.indonesian.txt) | Bahasa Indonesia | Indonesian | Unknown | [JSON](https://cdn.globalquran.com/quran_data/complete/json/id.indonesian.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/id.indonesian/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/id.indonesian/1.txt) |
| [`id.jalalayn`](translation/id.jalalayn.txt) | Tafsir Jalalayn _(draft)_ | Indonesian | Jalal ad-Din al-Mahalli and Jalal ad-Din as-Suyuti | [JSON](https://cdn.globalquran.com/quran_data/complete/json/id.jalalayn.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/id.jalalayn/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/id.jalalayn/1.txt) |
| [`id.muntakhab`](translation/id.muntakhab.txt) | Quraish Shihab | Indonesian | Muhammad Quraish Shihab et al. | [JSON](https://cdn.globalquran.com/quran_data/complete/json/id.muntakhab.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/id.muntakhab/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/id.muntakhab/1.txt) |
| [`it.piccardo`](translation/it.piccardo.txt) | Piccardo | Italian | Hamza Roberto Piccardo | [JSON](https://cdn.globalquran.com/quran_data/complete/json/it.piccardo.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/it.piccardo/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/it.piccardo/1.txt) |
| [`ja.japanese`](translation/ja.japanese.txt) | Japanese | Japanese | Unknown | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ja.japanese.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ja.japanese/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ja.japanese/1.txt) |
| [`ko.korean`](translation/ko.korean.txt) | Korean | Korean | Unknown | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ko.korean.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ko.korean/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ko.korean/1.txt) |
| [`ku.asan`](translation/ku.asan.txt) | ته‌فسیری ئاسان | Kurdish | Burhan Muhammad-Amin | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ku.asan.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ku.asan/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ku.asan/1.txt) |
| [`ml.abdulhameed`](translation/ml.abdulhameed.txt) | അബ്ദുല്‍ ഹമീദ് & പറപ്പൂര്‍ | Malayalam | Cheriyamundam Abdul Hameed and Kunhi Mohammed Parappoor | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ml.abdulhameed.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ml.abdulhameed/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ml.abdulhameed/1.txt) |
| [`ml.karakunnu`](translation/ml.karakunnu.txt) | കാരകുന്ന് & എളയാവൂര് _(draft)_ | Malayalam | Muhammad Karakunnu and Vanidas Elayavoor | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ml.karakunnu.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ml.karakunnu/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ml.karakunnu/1.txt) |
| [`ms.basmeih`](translation/ms.basmeih.txt) | Basmeih | Malay | Abdullah Muhammad Basmeih | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ms.basmeih.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ms.basmeih/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ms.basmeih/1.txt) |
| [`nl.keyzer`](translation/nl.keyzer.txt) | Keyzer | Dutch | Salomo Keyzer | [JSON](https://cdn.globalquran.com/quran_data/complete/json/nl.keyzer.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/nl.keyzer/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/nl.keyzer/1.txt) |
| [`nl.leemhuis`](translation/nl.leemhuis.txt) | Leemhuis _(draft)_ | Dutch | Fred Leemhuis | [JSON](https://cdn.globalquran.com/quran_data/complete/json/nl.leemhuis.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/nl.leemhuis/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/nl.leemhuis/1.txt) |
| [`nl.siregar`](translation/nl.siregar.txt) | Siregar _(draft)_ | Dutch | Sofian S. Siregar | [JSON](https://cdn.globalquran.com/quran_data/complete/json/nl.siregar.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/nl.siregar/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/nl.siregar/1.txt) |
| [`no.berg`](translation/no.berg.txt) | Einar Berg | Norwegian | Einar Berg | [JSON](https://cdn.globalquran.com/quran_data/complete/json/no.berg.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/no.berg/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/no.berg/1.txt) |
| [`pl.bielawskiego`](translation/pl.bielawskiego.txt) | Bielawskiego | Polish | Józefa Bielawskiego | [JSON](https://cdn.globalquran.com/quran_data/complete/json/pl.bielawskiego.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/pl.bielawskiego/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/pl.bielawskiego/1.txt) |
| [`ps.abdulwali`](translation/ps.abdulwali.txt) | عبدالولي _(draft)_ | Pashto | Abdulwali Khan | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ps.abdulwali.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ps.abdulwali/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ps.abdulwali/1.txt) |
| [`pt.elhayek`](translation/pt.elhayek.txt) | El-Hayek | Portuguese | Samir El-Hayek | [JSON](https://cdn.globalquran.com/quran_data/complete/json/pt.elhayek.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/pt.elhayek/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/pt.elhayek/1.txt) |
| [`ro.grigore`](translation/ro.grigore.txt) | Grigore | Romanian | George Grigore | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ro.grigore.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ro.grigore/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ro.grigore/1.txt) |
| [`ru.abuadel`](translation/ru.abuadel.txt) | Абу Адель | Russian | Abu Adel | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ru.abuadel.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ru.abuadel/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ru.abuadel/1.txt) |
| [`ru.kalam`](translation/ru.kalam.txt) | Калям Шариф _(draft)_ | Russian | Muslim Religious Board of the Republiс of Tatarstan | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ru.kalam.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ru.kalam/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ru.kalam/1.txt) |
| [`ru.krachkovsky`](translation/ru.krachkovsky.txt) | Крачковский | Russian | Ignaty Yulianovich Krachkovsky | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ru.krachkovsky.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ru.krachkovsky/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ru.krachkovsky/1.txt) |
| [`ru.kuliev-alsaadi`](translation/ru.kuliev-alsaadi.txt) | Кулиев + ас-Саади _(draft)_ | Russian | Elmir Kuliev (with Abd ar-Rahman as-Saadi's commentaries) | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ru.kuliev-alsaadi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ru.kuliev-alsaadi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ru.kuliev-alsaadi/1.txt) |
| [`ru.kuliev`](translation/ru.kuliev.txt) | Кулиев | Russian | Elmir Kuliev | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ru.kuliev.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ru.kuliev/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ru.kuliev/1.txt) |
| [`ru.muntahab`](translation/ru.muntahab.txt) | Аль-Мунтахаб | Russian | Ministry of Awqaf, Egypt | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ru.muntahab.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ru.muntahab/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ru.muntahab/1.txt) |
| [`ru.osmanov`](translation/ru.osmanov.txt) | Османов | Russian | Magomed-Nuri Osmanovich Osmanov | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ru.osmanov.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ru.osmanov/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ru.osmanov/1.txt) |
| [`ru.porokhova`](translation/ru.porokhova.txt) | Порохова | Russian | V. Porokhova | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ru.porokhova.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ru.porokhova/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ru.porokhova/1.txt) |
| [`ru.sablukov`](translation/ru.sablukov.txt) | Саблуков | Russian | Gordy Semyonovich Sablukov | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ru.sablukov.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ru.sablukov/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ru.sablukov/1.txt) |
| [`sd.amroti`](translation/sd.amroti.txt) | امروٽي | Sindhi | Taj Mehmood Amroti | [JSON](https://cdn.globalquran.com/quran_data/complete/json/sd.amroti.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/sd.amroti/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/sd.amroti/1.txt) |
| [`si.naseemismail`](translation/si.naseemismail.txt) | Naseem Ismail | Sinhala | Naseem Isamil and Masoor Maulana, Kaleel | [JSON](https://cdn.globalquran.com/quran_data/complete/json/si.naseemismail.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/si.naseemismail/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/si.naseemismail/1.txt) |
| [`so.abduh`](translation/so.abduh.txt) | Abduh | Somali | Mahmud Muhammad Abduh | [JSON](https://cdn.globalquran.com/quran_data/complete/json/so.abduh.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/so.abduh/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/so.abduh/1.txt) |
| [`sq.ahmeti`](translation/sq.ahmeti.txt) | Sherif Ahmeti | Albanian | Sherif Ahmeti | [JSON](https://cdn.globalquran.com/quran_data/complete/json/sq.ahmeti.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/sq.ahmeti/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/sq.ahmeti/1.txt) |
| [`sq.mehdiu`](translation/sq.mehdiu.txt) | Feti Mehdiu | Albanian | Feti Mehdiu | [JSON](https://cdn.globalquran.com/quran_data/complete/json/sq.mehdiu.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/sq.mehdiu/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/sq.mehdiu/1.txt) |
| [`sq.nahi`](translation/sq.nahi.txt) | Efendi Nahi | Albanian | Hasan Efendi Nahi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/sq.nahi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/sq.nahi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/sq.nahi/1.txt) |
| [`sv.bernstrom`](translation/sv.bernstrom.txt) | Bernström | Swedish | Knut Bernström | [JSON](https://cdn.globalquran.com/quran_data/complete/json/sv.bernstrom.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/sv.bernstrom/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/sv.bernstrom/1.txt) |
| [`sw.barwani`](translation/sw.barwani.txt) | Al-Barwani | Swahili | Ali Muhsin Al-Barwani | [JSON](https://cdn.globalquran.com/quran_data/complete/json/sw.barwani.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/sw.barwani/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/sw.barwani/1.txt) |
| [`ta.tamil`](translation/ta.tamil.txt) | ஜான் டிரஸ்ட் | Tamil | Jan Turst Foundation | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ta.tamil.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ta.tamil/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ta.tamil/1.txt) |
| [`tg.ayati`](translation/tg.ayati.txt) | Оятӣ | Tajik | AbdolMohammad Ayati | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tg.ayati.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tg.ayati/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tg.ayati/1.txt) |
| [`th.thai`](translation/th.thai.txt) | ภาษาไทย | Thai | King Fahad Quran Complex | [JSON](https://cdn.globalquran.com/quran_data/complete/json/th.thai.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/th.thai/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/th.thai/1.txt) |
| [`tr.ates`](translation/tr.ates.txt) | Süleyman Ateş | Turkish | Suleyman Ates | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tr.ates.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tr.ates/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tr.ates/1.txt) |
| [`tr.bulac`](translation/tr.bulac.txt) | Alİ Bulaç | Turkish | Alİ Bulaç | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tr.bulac.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tr.bulac/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tr.bulac/1.txt) |
| [`tr.diyanet`](translation/tr.diyanet.txt) | Diyanet İşleri | Turkish | Diyanet Isleri | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tr.diyanet.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tr.diyanet/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tr.diyanet/1.txt) |
| [`tr.golpinarli`](translation/tr.golpinarli.txt) | Abdulbakî Gölpınarlı | Turkish | Abdulbaki Golpinarli | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tr.golpinarli.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tr.golpinarli/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tr.golpinarli/1.txt) |
| [`tr.ozturk`](translation/tr.ozturk.txt) | Öztürk | Turkish | Yasar Nuri Ozturk | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tr.ozturk.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tr.ozturk/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tr.ozturk/1.txt) |
| [`tr.vakfi`](translation/tr.vakfi.txt) | Diyanet Vakfı | Turkish | Diyanet Vakfi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tr.vakfi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tr.vakfi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tr.vakfi/1.txt) |
| [`tr.yazir`](translation/tr.yazir.txt) | Elmalılı Hamdi Yazır | Turkish | Elmalili Hamdi Yazir | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tr.yazir.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tr.yazir/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tr.yazir/1.txt) |
| [`tr.yildirim`](translation/tr.yildirim.txt) | Suat Yıldırım | Turkish | Suat Yildirim | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tr.yildirim.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tr.yildirim/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tr.yildirim/1.txt) |
| [`tr.yuksel`](translation/tr.yuksel.txt) | Edip Yüksel | Turkish | Edip Yüksel | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tr.yuksel.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tr.yuksel/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tr.yuksel/1.txt) |
| [`tt.nugman`](translation/tt.nugman.txt) | Yakub Ibn Nugman | Tatar | Yakub Ibn Nugman | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tt.nugman.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tt.nugman/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tt.nugman/1.txt) |
| [`ug.saleh`](translation/ug.saleh.txt) | محمد صالح | Uyghur | Muhammad Saleh | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ug.saleh.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ug.saleh/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ug.saleh/1.txt) |
| [`ur.ahmedali`](translation/ur.ahmedali.txt) | احمد علی | Urdu | Ahmed Ali | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ur.ahmedali.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ur.ahmedali/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ur.ahmedali/1.txt) |
| [`ur.jalandhry`](translation/ur.jalandhry.txt) | جالندہری | Urdu | Fateh Muhammad Jalandhry | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ur.jalandhry.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ur.jalandhry/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ur.jalandhry/1.txt) |
| [`ur.jawadi`](translation/ur.jawadi.txt) | علامہ جوادی | Urdu | Syed Zeeshan Haider Jawadi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ur.jawadi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ur.jawadi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ur.jawadi/1.txt) |
| [`ur.junagarhi`](translation/ur.junagarhi.txt) | محمد جوناگڑھی | Urdu | Muhammad Junagarhi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ur.junagarhi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ur.junagarhi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ur.junagarhi/1.txt) |
| [`ur.kanzuliman`](translation/ur.kanzuliman.txt) | احمد رضا خان | Urdu | Ahmed Raza Khan | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ur.kanzuliman.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ur.kanzuliman/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ur.kanzuliman/1.txt) |
| [`ur.maududi`](translation/ur.maududi.txt) | ابوالاعلی مودودی | Urdu | Abul A'ala Maududi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ur.maududi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ur.maududi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ur.maududi/1.txt) |
| [`ur.najafi`](translation/ur.najafi.txt) | محمد حسین نجفی _(draft)_ | Urdu | Muhammad Hussain Najafi | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ur.najafi.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ur.najafi/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ur.najafi/1.txt) |
| [`ur.qadri`](translation/ur.qadri.txt) | طاہر القادری | Urdu | Tahir ul Qadri | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ur.qadri.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ur.qadri/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ur.qadri/1.txt) |
| [`uz.sodik`](translation/uz.sodik.txt) | Мухаммад Содик | Uzbek | Muhammad Sodik Muhammad Yusuf | [JSON](https://cdn.globalquran.com/quran_data/complete/json/uz.sodik.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/uz.sodik/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/uz.sodik/1.txt) |
| [`zh.jian`](translation/zh.jian.txt) | Ma Jian | Chinese | Ma Jian | [JSON](https://cdn.globalquran.com/quran_data/complete/json/zh.jian.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/zh.jian/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/zh.jian/1.txt) |
| [`zh.majian`](translation/zh.majian.txt) | Ma Jian (Traditional) | Chinese | Ma Jian | [JSON](https://cdn.globalquran.com/quran_data/complete/json/zh.majian.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/zh.majian/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/zh.majian/1.txt) |
| [`zh.mazhonggang`](translation/zh.mazhonggang.txt) | Ma Zhong Gang | Chinese | 马仲刚 | [JSON](https://cdn.globalquran.com/quran_data/complete/json/zh.mazhonggang.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/zh.mazhonggang/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/zh.mazhonggang/1.txt) |

#### Transliterations (3)

The Arabic text written in another script.

| ID (source file) | Name | Language | Translator / author | Read it (CDN) |
|---|---|---|---|---|
| [`en.transliteration`](Transliteration/en.transliteration.txt) | Transliteration | English | English Transliteration | [JSON](https://cdn.globalquran.com/quran_data/complete/json/en.transliteration.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/en.transliteration/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/en.transliteration/1.txt) |
| [`ru.transliteration`](Transliteration/ru.transliteration.txt) | Транскрипция _(draft)_ | Russian | Russian Transliteration | [JSON](https://cdn.globalquran.com/quran_data/complete/json/ru.transliteration.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/ru.transliteration/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/ru.transliteration/1.txt) |
| [`tr.transliteration`](Transliteration/tr.transliteration.txt) | Çeviriyazı | Turkish | Muhammet Abay | [JSON](https://cdn.globalquran.com/quran_data/complete/json/tr.transliteration.json) · [first ayah](https://cdn.globalquran.com/quran_data/verse/tr.transliteration/1.txt) · [surah 1](https://cdn.globalquran.com/quran_data/surah/tr.transliteration/1.txt) |

#### Audio (63 reciters)

Every reciter with each format, bit rate and mode it has. Click a link to listen (browsers play mp3 and ogg directly; GitHub cannot embed an audio player in a README). File names inside a folder follow the structure described under Audio below.

| ID | Reciter | Language | Format | Bit rate | Mode | Status | Listen |
|---|---|---|---|---|---|---|---|
| `ar.abdulbasitmujawwad` | Abdul Basit (Mujawwad) · عبد الباسط عبد الصمد (مجوّد) | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdulbasitmujawwad/mp3/128kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.abdulbasitmujawwad/mp3/128kbs/0.mp3) |
| `ar.abdulbasitmujawwad` | Abdul Basit (Mujawwad) · عبد الباسط عبد الصمد (مجوّد) | Arabic | ogg | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdulbasitmujawwad/ogg/64kbs/1.ogg) · [A'udhu](https://audio.globalquran.com/ar.abdulbasitmujawwad/ogg/64kbs/0.ogg) |
| `ar.abdulbasitmurattal` | Abdul Basit · عبد الباسط عبد الصمد (مرتّل) | Arabic | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdulbasitmurattal/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.abdulbasitmurattal/mp3/64kbs/0.mp3) |
| `ar.abdulbasitmurattal` | Abdul Basit · عبد الباسط عبد الصمد (مرتّل) | Arabic | mp3 | 192 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdulbasitmurattal/mp3/192kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.abdulbasitmurattal/mp3/192kbs/0.mp3) |
| `ar.abdulbasitmurattal` | Abdul Basit · عبد الباسط عبد الصمد (مرتّل) | Arabic | ogg | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdulbasitmurattal/ogg/64kbs/1.ogg) · [A'udhu](https://audio.globalquran.com/ar.abdulbasitmurattal/ogg/64kbs/0.ogg) |
| `ar.abdulbasitwarsh` | Abdul Basit (Warsh) · عبد الباسط عبد الصمد (ورش) | Arabic | mp3 | 128 kbps | versebyverse | incomplete | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdulbasitwarsh/mp3/128kbs/1.mp3) |
| `ar.abdullahbasfar` | Abdullah Basfar · عبد الله بصفر | Arabic | mp3 | 32 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdullahbasfar/mp3/32kbs/1.mp3) |
| `ar.abdullahbasfar` | Abdullah Basfar · عبد الله بصفر | Arabic | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdullahbasfar/mp3/64kbs/1.mp3) |
| `ar.abdullahbasfar` | Abdullah Basfar · عبد الله بصفر | Arabic | mp3 | 192 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdullahbasfar/mp3/192kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.abdullahbasfar/mp3/192kbs/0.mp3) |
| `ar.abdulsamad` | Abdul Samad · عبد الباسط عبد الصمد | Arabic | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdulsamad/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.abdulsamad/mp3/64kbs/0.mp3) |
| `ar.abdurrahmaansudais` | Abdurrahmaan As-Sudais · عبد الرحمن السديس | Arabic | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdurrahmaansudais/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.abdurrahmaansudais/mp3/64kbs/0.mp3) |
| `ar.abdurrahmaansudais` | Abdurrahmaan As-Sudais · عبد الرحمن السديس | Arabic | mp3 | 192 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdurrahmaansudais/mp3/192kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.abdurrahmaansudais/mp3/192kbs/0.mp3) |
| `ar.abdurrahmaansudais` | Abdurrahmaan As-Sudais · عبد الرحمن السديس | Arabic | ogg | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.abdurrahmaansudais/ogg/64kbs/1.ogg) · [A'udhu](https://audio.globalquran.com/ar.abdurrahmaansudais/ogg/64kbs/0.ogg) |
| `ar.ahmedajamy` | Ahmed ibn Ali al-Ajamy · أحمد بن علي العجمي | Arabic | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.ahmedajamy/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.ahmedajamy/mp3/64kbs/0.mp3) |
| `ar.ahmedajamy` | Ahmed ibn Ali al-Ajamy · أحمد بن علي العجمي | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.ahmedajamy/mp3/128kbs/1.mp3) |
| `ar.ahmedneana` | Ahmed Neana · أحمد نعينع | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.ahmedneana/mp3/128kbs/1.mp3) |
| `ar.akramalalaqimy` | Akram Al Alaqimy · أكرم العلاقمي | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.akramalalaqimy/mp3/128kbs/1.mp3) |
| `ar.alafasy` | Alafasy · مشاري راشد العفاسي | Arabic | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.alafasy/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.alafasy/mp3/64kbs/0.mp3) |
| `ar.alafasy` | Alafasy · مشاري راشد العفاسي | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.alafasy/mp3/128kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.alafasy/mp3/128kbs/0.mp3) |
| `ar.alafasy` | Alafasy · مشاري راشد العفاسي | Arabic | ogg | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.alafasy/ogg/64kbs/1.ogg) |
| `ar.aldosarywarsh` | Ibrahim Al-Dosary (Warsh) · إبراهيم الدوسري (ورش) | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.aldosarywarsh/mp3/128kbs/1.mp3) |
| `ar.alihajjajsuesy` | Ali Hajjaj Alsouissi · علي حجاج السويسي | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.alihajjajsuesy/mp3/128kbs/1.mp3) |
| `ar.alijaber` | Ali Jaber · علي جابر | Arabic | mp3 | 64 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.alijaber/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.alijaber/mp3/64kbs/0.mp3) |
| `ar.aljazaerywarsh` | Yassin Al-Jazaery (Warsh) · ياسين الجزائري (ورش) | Arabic | mp3 | 64 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.aljazaerywarsh/mp3/64kbs/1.mp3) |
| `ar.aymansowaid` | Ayman Sowaid · أيمن سويد | Arabic | mp3 | 64 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.aymansowaid/mp3/64kbs/1.mp3) |
| `ar.azizalili` | Aziz Alili · عزيز عليلي | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.azizalili/mp3/128kbs/1.mp3) |
| `ar.bukhatir` | Salaah AbdulRahman Bukhatir · صلاح بوخاطر | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.bukhatir/mp3/128kbs/1.mp3) |
| `ar.faresabbad` | Fares Abbad · فارس عباد | Arabic | mp3 | 64 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.faresabbad/mp3/64kbs/1.mp3) |
| `ar.ghamadi` | Ghamadi · سعد الغامدي | Arabic | mp3 | 40 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.ghamadi/mp3/40kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.ghamadi/mp3/40kbs/0.mp3) |
| `ar.hanirifai` | Hani Rifai · هاني الرفاعي | Arabic | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.hanirifai/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.hanirifai/mp3/64kbs/0.mp3) |
| `ar.hanirifai` | Hani Rifai · هاني الرفاعي | Arabic | mp3 | 192 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.hanirifai/mp3/192kbs/1.mp3) |
| `ar.hanirifai` | Hani Rifai · هاني الرفاعي | Arabic | ogg | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.hanirifai/ogg/64kbs/1.ogg) |
| `ar.hudhaify` | Hudhaify · علي بن عبد الرحمن الحذيفي | Arabic | mp3 | 32 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.hudhaify/mp3/32kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.hudhaify/mp3/32kbs/0.mp3) |
| `ar.hudhaify` | Hudhaify · علي بن عبد الرحمن الحذيفي | Arabic | mp3 | 64 kbps | versebyverse | incomplete | [Bismillah (1:1)](https://audio.globalquran.com/ar.hudhaify/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.hudhaify/mp3/64kbs/0.mp3) |
| `ar.hudhaify` | Hudhaify · علي بن عبد الرحمن الحذيفي | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.hudhaify/mp3/128kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.hudhaify/mp3/128kbs/0.mp3) |
| `ar.husary` | Husary · محمود خليل الحصري | Arabic | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.husary/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.husary/mp3/64kbs/0.mp3) |
| `ar.husary` | Husary · محمود خليل الحصري | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.husary/mp3/128kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.husary/mp3/128kbs/0.mp3) |
| `ar.husary` | Husary · محمود خليل الحصري | Arabic | ogg | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.husary/ogg/64kbs/1.ogg) · [A'udhu](https://audio.globalquran.com/ar.husary/ogg/64kbs/0.ogg) |
| `ar.husarymuallim` | Husary (Muallim) · محمود خليل الحصري (المعلم) | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.husarymuallim/mp3/128kbs/1.mp3) |
| `ar.husarymujawwad` | Husary (Mujawwad) · محمود خليل الحصري (مجوّد) | Arabic | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.husarymujawwad/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.husarymujawwad/mp3/64kbs/0.mp3) |
| `ar.husarymujawwad` | Husary (Mujawwad) · محمود خليل الحصري (مجوّد) | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.husarymujawwad/mp3/128kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.husarymujawwad/mp3/128kbs/0.mp3) |
| `ar.husarymujawwad` | Husary (Mujawwad) · محمود خليل الحصري (مجوّد) | Arabic | ogg | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.husarymujawwad/ogg/64kbs/1.ogg) · [A'udhu](https://audio.globalquran.com/ar.husarymujawwad/ogg/64kbs/0.ogg) |
| `ar.ibrahimakhbar` | Ibrahim Akhdar · إبراهيم الأخضر | Arabic | mp3 | 32 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.ibrahimakhbar/mp3/32kbs/1.mp3) |
| `ar.juhaynee` | Abdullah Awad Al-Juhany · عبد الله عواد الجهني | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.juhaynee/mp3/128kbs/1.mp3) |
| `ar.karimmansoori` | Karim Mansoori · كريم منصوري | Arabic | mp3 | 40 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.karimmansoori/mp3/40kbs/1.mp3) |
| `ar.khalefaaltunaiji` | Khalefa Al-Tunaiji · خليفة الطنيجي | Arabic | mp3 | 64 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.khalefaaltunaiji/mp3/64kbs/1.mp3) |
| `ar.khalidalqahtani` | Khalid Al-Qahtanee · خالد القحطاني | Arabic | mp3 | 192 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.khalidalqahtani/mp3/192kbs/1.mp3) |
| `ar.mahermuaiqly` | Maher Al Muaiqly · ماهر المعيقلي | Arabic | mp3 | 64 kbps | versebyverse | incomplete | [Bismillah (1:1)](https://audio.globalquran.com/ar.mahermuaiqly/mp3/64kbs/1.mp3) |
| `ar.mahermuaiqly` | Maher Al Muaiqly · ماهر المعيقلي | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.mahermuaiqly/mp3/128kbs/1.mp3) |
| `ar.mahmoudalialbanna` | Mahmoud Ali Al-Banna · محمود علي البنا | Arabic | mp3 | 32 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.mahmoudalialbanna/mp3/32kbs/1.mp3) |
| `ar.matroud` | Abdullah Al-Matroud · عبد الله المطرود | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.matroud/mp3/128kbs/1.mp3) |
| `ar.minshawi` | Minshawi · محمد صديق المنشاوي | Arabic | mp3 | 32 kbps | versebyverse | incomplete | [Bismillah (1:1)](https://audio.globalquran.com/ar.minshawi/mp3/32kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.minshawi/mp3/32kbs/0.mp3) |
| `ar.minshawi` | Minshawi · محمد صديق المنشاوي | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.minshawi/mp3/128kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.minshawi/mp3/128kbs/0.mp3) |
| `ar.minshawi` | Minshawi · محمد صديق المنشاوي | Arabic | ogg | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.minshawi/ogg/64kbs/1.ogg) · [A'udhu](https://audio.globalquran.com/ar.minshawi/ogg/64kbs/0.ogg) |
| `ar.minshawimujawwad` | Minshawy (Mujawwad) · محمد صديق المنشاوي (مجوّد) | Arabic | mp3 | 64 kbps | versebyverse | incomplete | [Bismillah (1:1)](https://audio.globalquran.com/ar.minshawimujawwad/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.minshawimujawwad/mp3/64kbs/0.mp3) |
| `ar.minshawimujawwad` | Minshawy (Mujawwad) · محمد صديق المنشاوي (مجوّد) | Arabic | mp3 | 192 kbps | versebyverse | incomplete | [Bismillah (1:1)](https://audio.globalquran.com/ar.minshawimujawwad/mp3/192kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.minshawimujawwad/mp3/192kbs/0.mp3) |
| `ar.minshawimujawwad` | Minshawy (Mujawwad) · محمد صديق المنشاوي (مجوّد) | Arabic | ogg | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.minshawimujawwad/ogg/64kbs/1.ogg) · [A'udhu](https://audio.globalquran.com/ar.minshawimujawwad/ogg/64kbs/0.ogg) |
| `ar.mohammadtablaway` | Mohammad al Tablaway · محمد الطبلاوي | Arabic | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.mohammadtablaway/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.mohammadtablaway/mp3/64kbs/0.mp3) |
| `ar.mohammadtablaway` | Mohammad al Tablaway · محمد الطبلاوي | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.mohammadtablaway/mp3/128kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.mohammadtablaway/mp3/128kbs/0.mp3) |
| `ar.muhammadabdulkareem` | Muhammad AbdulKareem · محمد عبد الكريم | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.muhammadabdulkareem/mp3/128kbs/1.mp3) |
| `ar.muhammadayyoub` | Muhammad Ayyoub · محمد أيوب | Arabic | mp3 | 32 kbps | versebyverse | incomplete | [Bismillah (1:1)](https://audio.globalquran.com/ar.muhammadayyoub/mp3/32kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.muhammadayyoub/mp3/32kbs/0.mp3) |
| `ar.muhammadayyoub` | Muhammad Ayyoub · محمد أيوب | Arabic | mp3 | 64 kbps | versebyverse | incomplete | [Bismillah (1:1)](https://audio.globalquran.com/ar.muhammadayyoub/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.muhammadayyoub/mp3/64kbs/0.mp3) |
| `ar.muhammadayyoub` | Muhammad Ayyoub · محمد أيوب | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.muhammadayyoub/mp3/128kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.muhammadayyoub/mp3/128kbs/0.mp3) |
| `ar.muhammadjibreel` | Muhammad Jibreel · محمد جبريل | Arabic | mp3 | 64 kbps | versebyverse | incomplete | [Bismillah (1:1)](https://audio.globalquran.com/ar.muhammadjibreel/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.muhammadjibreel/mp3/64kbs/0.mp3) |
| `ar.muhammadjibreel` | Muhammad Jibreel · محمد جبريل | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.muhammadjibreel/mp3/128kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.muhammadjibreel/mp3/128kbs/0.mp3) |
| `ar.muhsinalqasim` | Muhsin Al Qasim · عبد المحسن القاسم | Arabic | mp3 | 192 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.muhsinalqasim/mp3/192kbs/1.mp3) |
| `ar.mustafaismail` | Mustafa Ismail · مصطفى إسماعيل | Arabic | mp3 | 48 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.mustafaismail/mp3/48kbs/1.mp3) |
| `ar.nasseralqatami` | Nasser Alqatami · ناصر القطامي | Arabic | mp3 | 96 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.nasseralqatami/mp3/96kbs/1.mp3) |
| `ar.parhizgar` | Parhizgar · شهریار پرهیزگار | Arabic | mp3 | 48 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.parhizgar/mp3/48kbs/1.mp3) |
| `ar.sahlyassin` | Sahl Yassin · سهل ياسين | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.sahlyassin/mp3/128kbs/1.mp3) |
| `ar.salahalbudair` | Salah Al Budair · صلاح البدير | Arabic | mp3 | 192 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.salahalbudair/mp3/192kbs/1.mp3) |
| `ar.saoodshuraym` | Saood bin Ibraaheem Ash-Shuraym · سعود بن إبراهيم الشريم | Arabic | mp3 | 64 kbps | versebyverse | incomplete | [Bismillah (1:1)](https://audio.globalquran.com/ar.saoodshuraym/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.saoodshuraym/mp3/64kbs/0.mp3) |
| `ar.saoodshuraym` | Saood bin Ibraaheem Ash-Shuraym · سعود بن إبراهيم الشريم | Arabic | mp3 | 128 kbps | versebyverse | incomplete | [Bismillah (1:1)](https://audio.globalquran.com/ar.saoodshuraym/mp3/128kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.saoodshuraym/mp3/128kbs/0.mp3) |
| `ar.saoodshuraym` | Saood bin Ibraaheem Ash-Shuraym · سعود بن إبراهيم الشريم | Arabic | ogg | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.saoodshuraym/ogg/64kbs/1.ogg) |
| `ar.shaatree` | Abu Bakr Ash-Shaatree · أبو بكر الشاطري | Arabic | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.shaatree/mp3/64kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.shaatree/mp3/64kbs/0.mp3) |
| `ar.shaatree` | Abu Bakr Ash-Shaatree · أبو بكر الشاطري | Arabic | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.shaatree/mp3/128kbs/1.mp3) · [A'udhu](https://audio.globalquran.com/ar.shaatree/mp3/128kbs/0.mp3) |
| `ar.shaatree` | Abu Bakr Ash-Shaatree · أبو بكر الشاطري | Arabic | ogg | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ar.shaatree/ogg/64kbs/1.ogg) |
| `ar.yasersalamah` | Yaser Salamah · ياسر سلامة | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.yasersalamah/mp3/128kbs/1.mp3) |
| `ar.yasserdussary` | Yasser Ad-Dussary · ياسر الدوسري | Arabic | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ar.yasserdussary/mp3/128kbs/1.mp3) |
| `az.balayev` | Balayev · Balayev | Azerbaijani | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/az.balayev/mp3/128kbs/1.mp3) |
| `bs.korkut` | Besim Korkut · Besim Korkut | Bosnian | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/bs.korkut/mp3/128kbs/1.mp3) |
| `en.basfarwalk` | Abdullah Basfar and Ibrahim Walk | English | mp3 | 192 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/en.basfarwalk/mp3/192kbs/1.mp3) |
| `en.walk` | Ibrahim Walk | English | mp3 | 192 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/en.walk/mp3/192kbs/1.mp3) |
| `fa.hedayatfarfooladvand` | Fooladvand - Hedayatfar · فولادوند - هدایت‌فر | Persian | mp3 | 40 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/fa.hedayatfarfooladvand/mp3/40kbs/1.mp3) |
| `fa.kabirimakarem` | Makarem - Kabiri  · مکارم - کبیری | Persian | mp3 | 16 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/fa.kabirimakarem/mp3/16kbs/1.mp3) |
| `fr.leclerc` | Youssouf Leclerc · Youssouf Leclerc | French | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/fr.leclerc/mp3/128kbs/1.mp3) |
| `kk.altai` | Khalifah Altai · Халифа Алтай | Kazakh | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/kk.altai/mp3/128kbs/1.mp3) |
| `ru.kuliev` | Elmir Kuliev · Эльмир Кулиев | Russian | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ru.kuliev/mp3/128kbs/1.mp3) |
| `ru.kuliev2` | Elmir Kuliev (second reading) · Эльмир Кулиев (второе прочтение) | Russian | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ru.kuliev2/mp3/128kbs/1.mp3) |
| `tr.diyanet` | Diyanet Vakfi · Diyanet Vakfı | Turkish | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/tr.diyanet/mp3/128kbs/1.mp3) |
| `ur.hashmi` | Farhat Hashmi (word for word) · فرحت ہاشمی | Urdu | mp3 | 32 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/ur.hashmi/mp3/32kbs/1.mp3) |
| `ur.khan` | Shamshad Ali Khan · شمشاد علی خان | Urdu | mp3 | 64 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/ur.khan/mp3/64kbs/1.mp3) |
| `uz.sodik` | Muhammad Sodik Muhammad Yusuf · Мухаммад Содик Мухаммад Юсуф | Uzbek | mp3 | 128 kbps | versebyverse | draft | [Bismillah (1:1)](https://audio.globalquran.com/uz.sodik/mp3/128kbs/1.mp3) |
| `zh.chinese` | Chinese · 中文 | Chinese | mp3 | 128 kbps | versebyverse | active | [Bismillah (1:1)](https://audio.globalquran.com/zh.chinese/mp3/128kbs/1.mp3) |

<!-- LISTS:END -->
