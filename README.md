# bible-corpus
A multilingual parallel corpus created from translations of the Bible.

Here you can find a multilingual parallel corpus created from translations of the Bible.
This an effort to create a parallel corpus containing as many languages as possible that could be used for 
a number of NLP tasks. Using the Book, Chapter and Verse indices the corpus is aligned (almost) at a sentence level. 
(There are cases where two verses in one language are translated as one in another).

Following [a similar effort](http://www.umiacs.umd.edu/~resnik/parallel/bible.html) by Philip Resnik and Mari Broman 
Olsen at the University of Maryland, I have encoded the text of each language in XML files using the
[Corpus Encoding Standard](http://www.cs.vassar.edu/CES/). 
Refer to the following paper for more details about the creation of the corpus:

* [A massively parallel corpus: the Bible in 100 languages](http://link.springer.com/article/10.1007/s10579-014-9287-y),
Christos Christodoulopoulos and Mark Steedman, *Language Resources and Evaluation*, 49 (2)

[Armin Hoenen](https://www.hucompute.org/team/armin-hoenen) from the [Text Technology Lab](https://www.hucompute.org/) 
at the Goethe Universität, has created tokenised versions of four languages 
(Chinese, Japanese, Thai, Vietnamese). They are included in this collection but they can also be found 
[here](https://www.hucompute.org/ressourcen/corpora).

If you are looking for a quick way to generating a raw text version of each Bible, you can use following Python snippet (replace `lang` with the name of the XML file):
```
import xml.etree.ElementTree as ET
lang = 'English'
root = ET.fromstring(open(lang + '.xml').read())
with open(lang + '.txt', 'w', encoding='utf-8') as out:
    for n in root.iter('seg'):
        out.write(n.text.strip() + '\n')
```
or for a specific book:
```
book_id = 'b.GEN'
with open(lang + '-' + book_id + '.txt', 'w', encoding='utf-8') as out:
    for n in root.findall('.//div[@id="'+book_id+'"]/*seg'):
        out.write(n.text.strip() + '\n')
```

Follow this link for [a collection of tools for reading/processing the corpus](https://github.com/christos-c/bible-corpus-tools).
