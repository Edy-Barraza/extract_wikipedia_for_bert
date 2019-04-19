# Extract Wikipedia For BERT

Extract Wikipedia as a corpus suitable for pre-training on [Google's BERT model](https://github.com/google-research/bert). 
Running this process returns a txt file, where each sentence is written on a new line and each article is seperated by a line. 

Performing this task is a 3 step process! 
<ol type="I">
    <b>
    <li> Download Wikipedia Dump </li>
    <li> Run WikiExtractor.py </li>
    <li> Run extract_jsons.py </li>
    </b>
</ol>


<h3> I. Download Wikipedia Dump  </h3>
Go to https://dumps.wikimedia.org/ for a wide variety of dumps of Wikipedia's website. I prefer 
https://dumps.wikimedia.org/enwiki/latest/ for the latest dump. 

When working on my machine I prefer a smaller shard: `enwiki-latest-pages-articles1.xml-p10p30302.bz2`

But on cloud I prefer the whole dump: `enwiki-latest-pages-articles.xml.bz2`

<h3> II. Run WikiExtractor.py </h3>
The next step is to extract wikipedia in a form we can work with. Using the script wikiextractor/WikiExtractor.py, you run 

```
python WikiExtractor.py /dumppath/your_chosen_dump.bz2 --output /outputdir/ --json 
```
This script will extract Wikipedia for you, returning in the outputdir a series of folders. In each folder there will be a series of files.
This form is demonstrated as such:

```
/outputdir
├── /AA 
├── /AB
├── ...
└── /ZZ
    ├── wiki_00
    ├── ...
    └── wiki_99
    
```
Each file wiki_xx contains a JSON on each line in form:

```
{"id":"336","url": "https://en.wikipedia.org/wiki?curid=336", "title": "Altruism","text": "Altruism\n\nAltruism is the principle and moral practice of concern for happiness of other human beings and/or animals, resulting in a quality of life both material and spiritual..." } 
```

For more information on `WikiExtractor.py` checkout their [github page](https://github.com/attardi/wikiextractor)
<h3> III. Run extract_jsons.py </h3>
