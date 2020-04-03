# Requirements:

## System packages

- `Python 3.6+`
- `git`

## Installing Python dependencies

- `pip3 install requests sh click` 
- `pip3 install regex docopt numpy sklearn scipy`, if you want to use `classify_xvsy_logreg.py`
- `git clone git@github.com:sarnthil/unify-emotion-datasets.git`
```
conda install -c anaconda requests
conda install -c anaconda click
conda install -c anaconda docopt
conda install -c anaconda numpy
conda install -c anaconda scikit-learn
conda install -c anaconda scipy
conda install -c conda-forge sh
conda install -c conda-forge regex
```


This will create a new folder called `unify-emotion-datasets`.

# Running the two scripts

First run the script that downloads all obtainable datasets:

- `cd unify-emotion-datasets  # go inside the repository`
- `python3 download_datasets.py`


Please read carefully the instructions, you will be asked to read and confirm having read the licenses and terms of use of each dataset. 
In case the dataset is not obtainable directly you will be given instructions on how to obtain the dataset.

Then run the script that unifies the downloaded datasets, which will be located in `unify-emotion-datasets/datasets/`:

`python3 create_unified_dataset.py`


This will create a new file called `unified-dataset.jsonl` in the same folder.

Also, we advise you to cite the papers corresponding to the datasets you use.
The corresponding `bibtex` citations you find in the file `datasets/README.md` or while
running `download_datasets.py`. 

# Paper/Reference
[An Analysis of Annotated Corpora for Emotion Classification in Text](http://aclweb.org/anthology/C18-1179.pdf)

If you plan to use this corpus, please use this citation:

```
@inproceedings{Bostan2018,
  author = {Bostan, Laura Ana Maria and Klinger, Roman},
  title = {An Analysis of Annotated Corpora for Emotion Classification in Text},
  booktitle = {Proceedings of the 27th International Conference on Computational Linguistics},
  year = {2018},
  publisher = {Association for Computational Linguistics},
  pages = {2104--2119},
  location = {Santa Fe, New Mexico, USA},
  url = {http://aclweb.org/anthology/C18-1179},
  pdf = {http://aclweb.org/anthology/C18-1179.pdf}
}
```

## Experimenting with classification

If you want to reuse the code for the emotion classification task, see the script `classify_xvsy_logreg.py`:

 `python3 classify_xvsy_logreg.py --help` will show you the following: 

``` 
Classify using MaxEnt algorithm

Usage:
    classify_xvsy_logreg.py [options] <first> <second>
    classify_xvsy_logreg.py [options] --all-vs <second>

Options:
    -j --json=<JSONFILE>  Filename of the json file [default: ../unified.jsonl]
    -a --all-vs<=dataset> Dataset name of the testing data
    -d --debug            Use a small word list and a fast classifier
    -o --output=<OUTPUT>  Output folder [default: .]
    -m --force-multi      Force using multi-label classification
    -k --keep-last        Quit immediately if results file found
```
For example if you want to train on TEC and test on SSEC do the following:

    python3 classify_xvsy_logreg.py -d tec emoint 

The names of the dataset are the ones used in the file `unified-dataset.jsonl` in the field `source`.

# Tip
Use [`jq`](https://stedolan.github.io/jq/manual/) for an easy interaction with the `unified-dataset.jsonl`

Examples of how to use it for various tasks:
- selecting the instances of that have as a source `crowdflower` or `tec`
 `jq 'select(.source=="crowdflower" or .source =="tec")' <unified-dataset.jsonl | less `
- count how often instances are annotated with high surprise per dataset
`jq 'select(.emotions.surprise >0.5) | .source' <unified-dataset.jsonl | sort | uniq -c`
'''

# Selectec Sentences (10 sentences for each category)
- joy
- trust
- fear
- surprise
- sadness
- disgust
- anger
- anticipation

## joy
1. But Nutkin ran in front laughing, and shouting
2. Nutkin danced up and down like a sunbeam
3. He comes roaring up the land!
4. Then they squeaked with joy!
5. Shall we dear little muffins?
6. The cat family had quite recovered
7. The little mice only laghed
8. Mittens laughed so that she fell off the wall
9. It's a very fine morning!
10. Let us have a dinner party all to ourselves!
11. Come in good time, my dear Duchess
12. He sat and smiled
13. Your very good health
14. He think it is a very funny bird!
15. It was most kind to Timmy Tiptoes
16. I thank you kindly
17. Oh what a good idea!
18. I am glad I used the bottom oven
19. Oh what lovely flowers!
20. How good that pie smells!

## trust
1. Michelle Obama has the best arms
2. Revealed a lot about who he is as a man
3. Barak is luckly to have an intelligent woman
4. Don't forget to register to vote
5. Thank you for honoring the great workers
6. It's time to do some nation building right here
7. Honestly think America would benefit
8. You're my dude
9. Everyone needs to get the vote!
10. It's about what kind of difference you make!
11. What a tremendous patriot he is
12. His future is so bright
13. I am the hope you have been in search of
14. a true orator for our time
15. We are not going back we are moving forward
16. Am I seriously the only one who knows that
17. I just wanna cry at how amazing he is at what he does
18. That was such a good visual of what life could be
19. It is important to show Christ's love for all people
20. I support helping the needy

## fear
1. She seemed to be in a terrible fright.
2. Oh, my poor son Thomas!
3. Tom Kitten was getting very frightened!
4. It was most confusing in the dark.
5. Peter heard noises worse than ever.
6. A little frightened voice called out.
7. Peter was most dreadfully frightened.
8. He was out of breath and trembling with fright
9. Inside the house the racket was fearful.
10. He was afraid to go to sleep himself.
11. I can hear them clucking!
12. He began to walk frightfully lame
13. How they terrified the poor duckling!
14. Sleep was still in his eyes, but yet he crowed out
15. I was frightened, to be sure
16. The poor little elf was very much frightened
17. Driven by fear and horror, she flew homeward
18. He was of opinion that he had nothing to fear
19. The rats are eating her up alive!
20. There arose a very terrible storm

## surprise
1. This is very peculiar
2. What's that?
3. How could I have swallowed it!
4. Is it possible?
5. What pretty dancing shoes!
6. What does this mean?
7. What a quantity of gold there was!
8. Why are you lying up there?
9. Are you mad? they all cried
10. What a lucky fellow you are!
11. Oh, how his heart did best!
12. How she glittered!
13. What a rediculous little shoot!
14. Dear me! how singular
15. Oh dear, what was that?
16. It is dreadfully hot here!
17. Well, it's most abominably hot here
18. Oh, how cold the water is!
19. As if these things were of any consequence!
20. It is just what I expected!

## sadness
1. I'm in sad trouble
2. It feels sad
3. Peter began to cry
4. Tears stood in his eyes
5. Cried the little boy
6. It is all over with me
7. The old grandfather wiped his eyes
8. It made little tiny very sad to see it
9. Tears of sorrow rolled down their cheeks
10. There she stood and cried
11. Alas, unfortunate creature that I am!
12. Oh, how wretched I am!
13. Unfortunately I have not long to live
14. I long for it almost with pain
15. I am weary with longing
16. Oh! it is terrible lonely here
17. Poor little creature!
18. Oh, what bitter tears she shed!
19. And I often cried about you
20. Oh, I cannot bear it

## disgust
1. He shut his eyes obstinately
2. Old Mr. Brown turned up his eyes in disgust
3. It smells sooty
4. What a nasty person!
5. I must have a disinfecting
6. That is a dangerous woman
7. But he is so big and ugly
8. What an absurd idea
9. It is very naughty
10. That is tiresome
11. The neighbors declared it was unbearable
12. That was a terrible affair!
13. It is a horrible story
14. We think it is a very miserable story
15. There's a not a drop of malicious blood in me
16. You must not say that
17. This sight is really too tedious
18. and it looks miserable here
19. I was soon very tired of it
20. She has drunk herself to death

## anger
1. I do not think
2. You're a rude fellow
3. Go out of my sight
4. We will revenge ourselves
5. The young storks were very angry
6. It is stupid nonsense to allow yourself
7. Ignorance upon ignorance indeed!
8. Get away, don't come so near me
9. Everything in it is so stupid
10. I will destroy everything
11. You bad boy!
12. You wicked boy!
13. I don't understand your outlandish talk
14. His first feeling was one of anger
15. What a goose you are to do such silly things!
16. That is too bad!
17. How can you dare
18. Said she with angry look
19. You shall suffer for it!
20. Then the King grew angry

## anticipation
1. So looking forward to the debate tonight
2. I can't wait to vote
3. Getting ready for an exciting speech
4. Finally catching up all the speeches
5. Really fantastic video
6. I wonder what Barack would say
7. I am really looking forward to
8. Glad we will be in center for DNC
9. The best part of any election is just afterwards
10. We can do better!
11. Feels like yesterday I was here in Concord
12. I bought two pins one for me
13. Just got in my first political debate ever
14. Is anybody else excited for debates to start?
15. Anyone else find it weird?
16. I hope people have enough common sense
17. Consider what the world would be now
18. Things that are politically incorrect?
19. Don't know why but I am really looking forward to
20. Don't forget to watch CNN tonight.


