## Wikidata Lexicographical Coverage

This is a set of scripts to update the [Wikidata lexicographical coverage
pages](https://www.wikidata.org/wiki/Wikidata:Lexicographical_coverage).

## Setup

The generated missing lists can be copied manually or updated using `update-wiki.js`.
To use `update-wiki.js`, some additional setup is needed.
Otherwise, you can skip this section.

Install the dependencies:

```
npm install mwbot
```

Copy the example config file:

```
cp config.json.example config.json
```

Create a [bot password](https://www.wikidata.org/wiki/Special:BotPasswords)
and add the username and password to `config.json`.

## Run

Download and parse the corpus files.
These only need to be run once unless new languages are added.
The download script will skip downloading any existing files but the parsing
script will reparse the files each time it is run, which takes a while.

```
python3 corpora-download.py
python3 corpora-parse.py
```

Download and parse the latest lexeme data dump.
Dumps are currently produced weekly.
The download script will skip downloading the dump if the remote file is not
newer than the local one.
The parsing script will reparse the file each time it is run.


```
python3 dump-download.py && python3 dump-parse.py
```

Generate statistics and missing word lists.

```
python3 generate-statistics.py
python3 generate-missing-lists.py
```

Update the statistics and missing lists on wiki.

```
node update-wiki.js
```

## Additional information

All of the scripts (with the exception of `dump-download.py` for hopefully
obvious reasons) support being passed a subset of language codes as
command-line parameters, e.g. to download only the German corpus file:

```
python3 corpora-download.py de
```

