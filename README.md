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
https://dumps.wikimedia.org/enwiki/latest/ for the latest dump. Choose a dump that suits your needs.
When working on my machine I prefer:

```
enwiki-latest-pages-articles1.xml-p10p30302.bz2 
```

but on cloud I prefer the whole dump: 

```
enwiki-latest-pages-articles.xml.bz2 
```

<h3> II. Run WikiExtractor.py </h3>

<h3> III. Run extract_jsons.py </h3>
