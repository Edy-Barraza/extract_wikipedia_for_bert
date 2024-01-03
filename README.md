# Extract Wikipedia For BERT

Extract Wikipedia as a corpus suitable for pre-training on [Google's BERT Transformer model](https://github.com/google-research/bert). 
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

The next step is to extract wikipedia in a form we can work with. Using the script `/wikiextractor/WikiExtractor.py`  you run 

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
Each file `wiki_xx` contains a JSON on each line in form:

```
{"id":"336","url": "https://en.wikipedia.org/wiki?curid=336", "title": "Altruism","text": "Altruism\n\nAltruism is the principle and moral practice of concern for happiness of other human beings and/or animals, resulting in a quality of life both material and spiritual..." } 
```

For more information on `WikiExtractor.py` checkout their [github page](https://github.com/attardi/wikiextractor)

<h3> III. Run extract_jsons.py </h3>

We now have everything we need to create our txt file for training the BERT transformer model! Let's run:

```
python extract_jsons.py --folder /folderof/foldersof/jsons/ --write_file /filepath/write_file.txt 
```

`extract_jsons.py` has the following arguments:

```
Args:
    folder (str): the folder containing the folders of wikipedia jsons we just previously created from running WikiExtrator.py
    write_file (str) : the txt file we will be writing to 
```

After extracting Wikipedia, you should have a txt file of ~12GB in size. To prepare this text for TensorFlow, we must turn it into a tfrecord file. tfrecord files allow us to work with a dataset when we can't load all of it onto RAM. As an intermediary step, we must first slit this file into smaller ones in order not to run into RAM or disk space problems later down the line. Thus we must run split_text.py

```
python split_text.py --read_file wikipedia.txt --split_number 20 --folder data/split_dir --name_base wiki_split
```
split_text.py has the following arguments:

```
Args:
    read_file (str) : the txt file that will be split
    split_number (int) : the number of smaller txt files that will be created
    folder (str) : the path where the split txt files will be placed
    name_base (str) : the base name of the split txt files. files will be named as such: base_name_N where N is a number
```

With that you will have Wikipedia in txt files all in one directory, ready to serve your training needs! 
