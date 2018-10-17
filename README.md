# PHOIBLE Scripts

The scripts in this repo use Python 3 and depend on `sqlite3`.

## Search

Use `search.py` to search PHOIBLE. 

A search query is minimally composed of a *search term*. There are two types of search terms. 

A *phoneme term* consists of a phoneme enclosed in forward slashes, optionally preceded by "no". This will find all doculects that have (or don't have, if there's a preceding "no") the given phoneme. 

For example, `/t̪ʙ/` will return all doculects that contain the phoneme represented in PHOIBLE by the text string `t̪ʙ`, and `no /m/` will return all doculects that do not contain the phoneme represented in PHOIBLE by the text string `/m/`.

A *feature term* consists of a number (optionally preceded by a `<` or `>` sign), a space, and a string of pluses and minuses followed (with no intervening space) by the name of the feature to search. For example, `2 +coronal` will return all doculects with exactly two [+coronal] segments, and `>30 +syllabic` wil return all doculects with more than thirty vowels.

Search terms may be joined by the logical operators `and` and `or`. These are postfix.

### Examples

Find doculects with only two coronal consonants
```
>python search.py "2 +coronal"
    HAWAIIAN
    PIRAHA
    ROTOKAS
    Pirahã
```

Find doculects with two or fewer vowels
```
>python search.py "<3 +syllabic"
    zulgo
    Cuvok
    Buwal
```
    
Find doculects with two or fewer vowels or the phoneme /ʰd/
```
>python search.py "<3 +syllabic /ʰd/ or"
    zulgo
    Cuvok
    Buwal
    Günün Yajich
    Hoti
```

Find doculects with no rounded segments
```
>python search.py "no +round"
    Oneida
    NIMBORAN
    Gu'de
```

Find doculects with /ʰd/ and no /m/
```
>python search.py "/ʰd/ no /m/ and"
    Hoti
```

## Import data

`import_inventories.py` and `import_segments.py` will import the data contained in `phoible-phonemes.tsv` and `phoible-segments-features.tsv` respectively (which must be in the same directory as the script, with these filenames) into a SQLite database `phoible.sqlite`. A pre-built database is included in this repo.

These scripts require `inflections` in addition to `sqlite3`.
