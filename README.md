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


