[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)


# Semantic Space and Size: a Proof-of-Concept for Exploring Cultural Bias on Very Small Corpora Using Cosine Similarity and Word2Vec*

### By <a href="https://disesdi.github.io/contact.html" target="_blank" rel="noopener noreferrer">Disesdi</a> | *2023/01/01*

-------

### *Code available [here >>](https://github.com/IndigenousEngineering/small_corpora_bias_with_w2v/blob/master/notebooks/small_corpora_bias_analysis_1.ipynb)*

-------

*__note:__ this post contains references to offensive language found in alt-right and other subreddits, including assault, gendered insults & profanity. links to subreddits, as well as corpora from subreddits used in this project, may also include offensive material.*


In 2017, [Caliskan et al](https://purehost.bath.ac.uk/ws/portalfiles/portal/168480066/CaliskanEtAl_authors_full.pdf) published their Word Embedding Association Test (WEAT), which explored relationships similar to those in the [Implicit Association Test (IAT)](https://implicit.harvard.edu/implicit/iatdetails.html) in GloVe word embedding models, using words as subjects rather than people. Using [cosine similarity](http://www.minerazzi.com/tutorials/cosine-similarity-tutorial.pdf) as a measure for correlation and stand-in for the IAT’s reaction time, the authors were able to replicate a number of well-known social biases.

I [wrote about this paper before](https://indigenousengineering.github.io/blog/posts/what_words_mean.html), including one aspect the authors introduce that I found particularly fascinating: 

> *...our methods could be used to quickly find differences in bias between demographic groups, given large corpora authored by members of the respective groups. If substantiated through testing and replication, WEAT may also give us access to implicit associations of groups not available for testing, such as historic populations.*

The possibility of using word embeddings and cosine similarity to explore the potential linguistic biases of historic cultures was extremely exciting to me! But the caveat was that in order to successfully train a model (which would in turn produce useful word associations), one would need a large enough corpus. In the case of historic populations, this necessarily limits research possibilities to corpora that have been lucky enough to have been preserved. 

This gave me pause, as historically scholarship around preservation of any type has often been carried out through a lens of western interests. How profoundly would the dominance of eurocentrism and colonialist scholarship shape the availability of historic corpora for study? And in the case of corpora that did survive, what qualities would they need? How large is large enough?

The answer to the first of those questions remains to be seen. But in terms of sussing out whether small or fragmented document collections would be workable for cosine similarity analysis, it seemed potentially useful to put together a toy model.

Thinking about this problem led me to a more precise question: on exactly how small a corpus could a word2vec model be reasonably expected to encode artifacts of culture? I decided to put together some code to test the usefulness of cosine similarity comparison on a few small, contemporary texts, just to see what I could find out.

#### how small is small?

The GloVe embeddings used in the WEAT paper were trained on the [Common Crawl](http://commoncrawl.org/) corpus. This corpus contains over 800 billion words, and after adjusting for case, 2.2 million unique tokens.

In contrast, the largest corpus I created and tested was taken from [Reddit](https://www.reddit.com/), specifically the subreddit r/KotakuInAction, and contains only 34,440 total tokens (8,471 unique words). The smallest corpus I tested was less than a quarter the size of r/KotakuInAction: at only 7,737 total words, it is taken from the r/Conservative subreddit, and allowed a model to find relationships among only 3,403 unique vocabulary words. 

Total word & unique vocabulary counts for the six corpora are listed in the table below:



| corpus source     | total vocabulary | unique words |
|------------------|-------------|--------------|
| r/KotakuInAction | 34,440      | 8,471        |
| r/The_Donald     | 23,412      | 6,478        |
| r/esist          | 18,156      | 5,576        |
| r/feminism       | 15,372      | 5,050        |
| r/Liberal        | 12,374      | 4,504        |
| r/Conservative   | 7,737       | 3,403        |


#### methods 

My goal was to minimize processing as much as I could--to test what could be accomplished with the bare minimum of corpus/vocabulary size, and text preparation. To that end, I decided to experiment on texts directly from Reddit, using standard python libraries and packages.

I chose to use Reddit for several reasons. I needed clearly-defined cultures with their own terminologies and specific associations. Political Reddit was a natural choice. 

In terms of subreddits with strong, publicly-stated and easily identifiable viewpoints, it would be difficult to beat [r/The_Donald](https://www.reddit.com/r/The_Donald/).

In 2017 FiveThirtyEight’s Trevor Martin wrote [an article](https://fivethirtyeight.com/features/dissecting-trumps-most-rabid-online-following/) calling r/The_Donald “Trump’s Most Rabid Online Following”, and “the epicenter of Trump fervor on the internet”. Applying latent semantic analysis to map subreddits based on their comments, the article documents the previously-disparate groups that coalesced to push Trump to victory using a coordinated strategy of trolling & [meme wars](https://motherboard.vice.com/en_us/article/xyvwdk/meme-warfare).

Later that year, Tim Squirrel [further documented](https://qz.com/1056319/what-is-the-alt-right-a-linguistic-data-analysis-of-3-billion-reddit-comments-shows-a-disparate-group-that-is-quickly-uniting/) r/The_Donald’s emerging unification of the far-right in Quartz, with graphs visualizing the changing usage, spread, and coalescence of far-right slang via r/The_Donald. A number of terms I tested are taken from these articles.

__Besides r/The_Donald, I chose five other politically polarized subreddits__, including two additional right-leaning subreddits: [r/Conservative](https://www.reddit.com/r/conservative/) and [r/KotakuInAction](https://www.reddit.com/r/KotakuInAction/). The latter constitutes the largest corpus, and is known as home to the notorious [GamerGate](https://en.wikipedia.org/wiki/Gamergate_controversy) movement. For balance, I added the left-leaning [r/Liberal](https://www.reddit.com/r/Liberal/), [r/esist](https://www.reddit.com/r/esist/), and [r/feminist](https://www.reddit.com/r/Feminism/).

Not all terms documented in the Quartz article appear in my cleaned vocabularies, but a number of them do--some with relationships that seem to correlate with what one might expect given social/cultural domain knowledge of far-right and left-wing political leanings. It’s worth noting that both the FiveThirtyEight and Quartz articles referenced above analyze vastly more content than my Reddit scraping, and even terms that are in wide usage are not guaranteed to be in the top-voted posts, *per se* (since these posts' popularity has nothing to do with statistical measures of the relative vocabularies). Nevertheless, the terms that did appear allowed me to replicate some neat expected relationships.

I chose some terms based on their potential to act as controls for other concepts. For example, I was loosely attempting to measure political “bias” *vis-à-vis* various subreddits’ attitudes towards 2016 US presidential candidates. In order to eliminate the possibility of noise from gendered associations--or just good old-fashioned sexism--I added the terms ‘men’ and ‘women’. This was intended to allow me to check whether a word that was associated with a particular candidate was also strongly associated with that candidate’s gender.

Another small check in the testing vocabulary is the addition of ‘sanders’, intended to represent US Senator and 2016 presidential candidate Bernie Sanders. Although I’m primarily interested in comparisons between ‘trump’ and ‘clinton’, because these are polar along a number of vectors--and cultural associations with Senator Sanders’ candidacy are arguably less well-defined than those of Clinton or Trump--to the extent that Sanders’ gender is encoded into the model, his last name can also help to check for gendered associations (versus those specific to the candidates themselves). 

I consider this one to be less reliable, for three reasons: first, the aforementioned murkiness of what Sanders’ candidacy meant to both the right and the left; second, ‘sanders’ is a proper noun, and while I felt it likely that in political subreddits this token would be attached to Candidate/Senator Sanders, I did not test to see what other associations ‘sanders’ might have. The models could be picking up some other noise. Third, another vocabulary concern enters in that Senator Sanders is also very likely to be referred to by his first name, “Bernie”; but adding ‘bernie’ to my terms tested would have ushered in more potentially confounding data, defeating the whole point of a simple check. So I humbly request that you take ‘sanders’ for what it’s worth.

Terms tested, and the subreddits in which they occur, are given in the table below:



| * indicates term present     | r/KotakuInAction | r/The_Donald | r/esist | r/feminism | r/Liberal | r/Conservative |
|:----------------------------:|:----------------:|:------------:|:-------:|:----------:|:---------:|:--------------:|
|             'fox'            |         *        |       *      |    *    |      *     |     *     |        *       |
|            'flynn'           |         _        |       *      |    *    |      _     |     *     |        _       |
|          'manafort'          |         _        |       _      |    *    |      _     |     *     |        *       |
|            'cuck'            |         _        |       *      |    _    |      _     |     _     |        _       |
|            'pepe'            |         *        |       *      |    _    |      _     |     _     |        _       |
|             'god'            |         *        |       *      |    *    |      *     |     *     |        *       |
|           'emperor'          |         _        |       *      |    _    |      _     |     _     |        _       |
|            'bitch'           |         *        |       *      |    *    |      *     |     _     |        _       |
|            'alpha'           |         *        |       *      |    _    |      _     |     _     |        _       |
|        'establishment'       |         *        |       *      |    *    |      _     |     _     |        _       |
|            'soros'           |         *        |       *      |    _    |      _     |     _     |        _       |
|           'prison'           |         *        |       *      |    *    |      *     |     *     |        *       |
|            'email'           |         *        |       *      |    *    |      _     |     *     |        *       |
|           'corrupt'          |         *        |       *      |    *    |      _     |     *     |        *       |
|            'good'            |         *        |       *      |    *    |      *     |     *     |        *       |
|            'evil'            |         *        |       *      |    *    |      *     |     _     |        _       |
|            'smart'           |         *        |       *      |    *    |      *     |     *     |        _       |
|           'assault'          |         *        |       *      |    *    |      *     |     *     |        *       |
|           'honest'           |         *        |       *      |    _    |      *     |     *     |        _       |
|           'brains'           |         *        |       *      |    _    |      *     |     _     |        _       |
|          'president'         |         *        |       *      |    *    |      *     |     *     |        *       |
|          'feminist'          |         *        |       *      |    _    |      *     |     _     |        *       |



Reddit was also a natural choice due to its ease of API access. Posts are easy to get: [PRAW](https://praw.readthedocs.io/en/latest/) makes downloading an entire subreddit simple. Depending on what methods you use, you can get posts ranked by “upvotes”. This is the method I chose, as I felt it allowed the community to curate its own documents. I took the top 1000 posts by upvote from each subreddit tested.

Given the community-curated aspect, I felt that political subreddits could serve as useful & somewhat responsible microcosms of culture. At the very least, they would provide well-defined vocabularies, and assumptions that could be easily tested against expectations given each subculture’s public self-expression. 

Another reason for choosing Reddit was that outside cultural analysis is always a dicey undertaking, particularly for one lone researcher with limited knowledge or expertise--like me! But political Reddit is fairly low stakes, as membership in the culture is self-selecting, and beliefs are centered around publicly held & promoted statements of identity. In other words: subreddit participation is voluntary, and chosen based on beliefs that people want to publicly share--so using their own words to analyze their biases seems like fair game. However, the implications of using this technology on corpora from historic & historically marginalized cultures cannot be discounted; I discuss some of these later in this post.

While I exploited common socio-political knowledge (and some research) to choose the terms I tested, I went fairly light on analyzing what these mean within each culture. My objective here was not to provide a probing and layered analysis of these subcultures; rather the intention was to create a proof-of-concept for cosine similarity analysis on relatively small and/or fragmented corpora--in this case, contemporary subcultures with reasonably predictable associations (for ease of testing).

I specifically chose to use political themes to test, rather than concepts from the Implicit Associations Test (as the WEAT paper did) for a couple of reasons. First and foremost, the aforementioned ease of verification means that by replicating associations that could be considered public domain knowledge about US politics, I would have an arguably more solid demo than say, inferences about less publicly held biases and beliefs. Eg, it’s safe to say that Hillary Clinton is not well liked on r/The_Donald without offering much evidence, but inferences around more general attitudes & cultural phenomena would, in my view, require much more data to be valid as models. Any associations not easily tested (or possibly disproven) could always be called into question due to the small size of the corpora; but if word2vec models were able to find similarities in concepts that match these political subcultures’ publicly stated values--on so little text--that might be something to consider.

Second, it seems easy to infer at least some of the implicit biases of these groups--and depending on one’s political views, it might well be. But because such inferences could reasonably be questioned due precisely to the small size of the training set, it would be irresponsible to throw the perceived authority of “AI” behind a sloppy inquiry where cultural judgements are on the line. Determining that in the right-wing subreddit r/The_Donald, ‘clinton’ is closer to ‘prison’ than is ‘trump’, however, is much lower-stakes, more easily verifiable (at least intuitively), and if I’m being honest, fascinating to be able to replicate.

#### text processing and word2vec model specs

All in all, text preparation was fairly minimal. I removed non-alpha characters and punctuation. I initially did not filter stopwords, but eventually found I got better model performance when stopwords were removed. I converted all tokens to lowercase, which obviously reduced the overall training vocabulary as well. I also prepared a version of each subreddit’s top vocabulary (sans stopwords), to hopefully provide a more useful analysis of frequent vocabulary words. 

Reddit posts can often be relatively short. For the purpose of model training, I treated each post as a sentence. To maximize available text, I also included (clean) titles, each treated as its own sentence. Text cleaning yielded between 1,000 to 2,000 sentences of varying length per subreddit.

Although the original paper uses [GloVe embeddings](https://nlp.stanford.edu/projects/glove/), I chose to use [word2vec](https://arxiv.org/pdf/1301.3781.pdf) (see [this paper also](https://arxiv.org/abs/1310.4546)), because it is arguably the simplest to implement. All model training and cosine comparison is done using python and [Gensim](https://radimrehurek.com/gensim/models/word2vec.html). In the spirit of the original paper, all model parameters are out-of-the-box: no special tuning was done. Due to the small size of each corpus, I allowed the models to train on words used only once.

Because of the stochastic nature of neural nets, I trained a total of three models per subreddit, retrieved their cosine similarities, then took the mean cosine similarity for each word tested. These are the final results I report.

Did I cherry-pick word pairs whose distances validated my assumptions? Yes, I absolutely did! You could easily break any assumptions with the right word pair--with only a few thousand words, these corpora are tiny. I personally find the relationships that *are* present here, even in so little data, to be pretty fascinating! If you’d like to try to break my models, you can find all the code [here on github](https://github.com/neurodivergent-ai/WEAT_analysis_1).

One final warning: for the next few paragraphs, everything is relative! Meaning I will be playing *very* fast and loose with numbers...so if that kind of thing makes you squeamish, it’s not too late to turn back now, and maybe [read something else I wrote](https://www.diverge.ai/#2).

#### results

Despite the (*very*) small sizes of the corpora, I was able to replicate a number of relationships. The key limitation was the available vocabulary--which I hypothesize is smaller in corpora harvested from Reddit than, say, corpora of similar size from formal literature, due to the compact and repetitive nature of meme-driven culture and, for lack of a more concise descriptor, internet slang.

*’god’*

Some patterns require looking a bit beneath the surface. For example, in all but one subreddit tested, ‘trump’ had an oppositional relationship to the word ‘god’. The exception to this was the extremely pro-Trump r/The_Donald, where the relationship between ‘trump’ and ‘god’ is a positive--albeit distant--one. Does this reflect a cultural perception of Trump as pious within r/The_Donald’s online subculture? Or could it instead be attributable the fact that the phrase “God Emperor Trump”--a semi-ironic invocation of divine mandate--is a favorite alt-right reference? 

The word ‘emperor’ appears only in r/The_Donald’s corpus, where it is far closer to ‘trump’ than to ‘clinton’. It’s entirely possible that this could be attributable to gendered language, and association of “emperor” with male rulers. Since ‘emperor’ also shows up closer to ‘sanders’ than ‘clinton’, this seems like a reasonable argument to make--but in my opinion, this also brings up the some of the problems with inferring causality: does ‘emperor’ show up nearer to ‘sanders’ because it’s a “male” word, or because it is Trump’s word, and ‘sanders’ happens (perhaps due to gender) to be nearer to ‘trump’ than is ‘clinton’? It’s difficult to say, and difficult to decide how to sort it out.

Given the phrase’s prevalence within alt-right communities, and the anomalous behavior of ‘trump’ vs ‘god’ in this corpus, It seems reasonable to consider that the phrase “God Emperor” might play a role here --especially when taking into account domain knowledge around the religiosity of r/The_Donald. This subreddit is known for being far more alt-right than religious-right. These factors lead me to suspect that within the culture of r/The_Donald, the phrase itself matters more than how religious Trump is perceived to be by this particular segment of the alt-right base.

Back to ‘god’: in both r/feminism and r/KotakuInAction, ‘god’ is closer to the right than the left; its relationship to ‘conservative’ is positive, if distant, while its relationship to ‘liberal’ is oppositional. 

In fact, in every subreddit tested--even the left-leaning r/esist, r/feminism, and r/Liberal--the word ‘god’ had a positive relationship with the word ‘conservative’, while in all six of the subreddits’ corpora, ‘god’ had either an oppositional, or positive-but-comparatively-distant, relationship with the word ‘liberal’. I interpret this as reflective of the central role that religion, and particularly the religious right, continue to play in US politics. 

Once the models were trained, several other interesting relationships emerged.

*‘flynn’, ’manafort’*

The names ‘flynn’ and ‘manafort’ are references to Michael Flynn and Paul Manafort, two prominent figures in the ongoing Mueller/Trump/Russia investigation. They do not appear in every subreddit’s vocabulary; in fact the only subreddits containing both names are r/Liberal and r/esist, both of which are primarily left-leaning groups (their absence from from left-leaning r/feminism could be explained by the group’s less overt focus on politics & political strategy versus social issues). 

Interestingly, these names did not appear together in any of the top-rated pro-Trump subreddits--although in r/Conservative, ‘manafort’ appears alone, and in much closer relation to both ‘trump’ and ‘conservative’ than any other words. The association of these names with ‘trump’ is replicated in both left-leaning subreddits where they appear together: in r/Liberal ‘flynn’ and ‘trump’ come in at 0.030927 versus ‘sanders’ at 0.008057 and ‘clinton’ with an oppositional -0.20109; ‘manafort’ & ‘trump’ are closer at 0.060389 than ‘manafort’ & clinton, at 0.010911. In r/esist, ‘trump’ beats ‘clinton’ for proximity to ‘manafort’ by a relatively not-insignificant 0.258156 to 0.080660, respectively.

And for r/esist redditors, associations for ‘clinton’ were in opposition with those for ‘flynn’, with a cosine similarity of -0.134861, while the similarity between ‘trump’ and ‘flynn’ was 0.223245. The strong associations of these names for left-leaning redditors, combined with their relative absence from the top-voted discourse on the right, potentially reflect the right’s perception of references to ‘flynn’ and ‘manafort’ as left-wing talking points (aka “fake news”). 

*‘fox’*

My hypothesis was that for most political subreddits, ‘fox’ would be associated with Fox News, and thus expected to correlate in some way with conservatism and/or ‘trump’. 

However, within all three right-leaning subreddits, ‘fox’ was more strongly associated with ‘clinton’ than ‘trump’. In trying to figure this out, I went back to my results, checking the relationships between ‘fox’ and the other terms I’d chosen to test. 

Given this information, I can come up with at least one solid Occam-worthy reason for this counterintuitive result: in a word, *sexism*. I noticed that in all but one of the corpora tested, ‘fox’ shared a positive relationship with the word ‘women’--and an oppositional one with the term ‘men’. This seems to point to the word’s strong associations as a gendered descriptor.

Traces of the association of ‘fox’ with conservatism appear elsewhere, though. In r/feminism, ‘fox’ shares a positive, if distant, relationship with ‘conservative’--versus the oppositional relationship it shares with ‘liberal’. And in r/Liberal, the cosine similarity between ‘fox’ and ‘liberal’ is a positive 0.00866, while the similarity between ‘fox’ and ‘conservative’ is a relatively stronger 0.1254.

In five out of six subreddit corpora, the following pattern emerged: ‘fox’ relates more noticeably with ‘conservative’ vs ‘liberal’, ‘clinton’ vs ‘trump’, and ‘women’ vs ‘men’. Despite the conservative associations with Fox News, in most of the corpora tested ‘fox’ is a gendered word.

The redditors of r/Resist provide a notable exception here. While still maintaining the gender-divided similarity differential between ‘fox’ and ‘women’ vs ‘fox’ and ‘men’ (0.345 vs -0.0113, respectively), candidate associations with the word tend definitively towards ‘trump’. It would appear that the redditors of r/esist believe Fox News has played at least some role in Donald Trump’s political ascension and/or governance. 

Again, the gendered association of the word across all corpora tested seems clear. However, adding nuance to the distinctions along the axes of gender versus political party: in both r/feminism and r/Liberal, ‘sanders’ is closer to ‘fox’ than either ‘clinton’ or ‘trump’, causing me to wonder whether these left-leaning subreddits in some way(s) group Sanders in more conservative company than they do Clinton.

(It  should be noted here that foxes are also animals, and not just cable news networks or bits of derogatory slang--but I did not test to see how close ‘fox’ is to say ‘dog’ or ‘squirrel’ or ‘forest’ or ‘hunter’, for that matter.)

*‘pepe’*

A reference to online comic character [Pepe the Frog](https://www.latimes.com/politics/la-na-pol-pepe-the-frog-hate-symbol-20161011-snap-htmlstory.html), the word ‘pepe’ appears in only two corpora: r/The_Donald, and r/KotakuInAction. It’s not surprising that ‘pepe’ appears here, as both of these subreddits are known for their meme activity, and Pepe the Frog was a central character in the rise of the alt-right online. In both subreddits, ‘pepe’ is far closer to ‘trump’ than to either ‘sanders’ or ‘clinton’. Regardless of the character’s previous history, it’s difficult to deny that Pepe is seen as a mascot of sorts by meme generators and consumers in the alt-right.

*‘bitch’*

The word ‘bitch’ appears in four out of six corpora, and there are a couple of noteable associations. In three of the four subreddits where it appears, including both the left-leaning r/feminism and r/esist, ‘bitch’ is much more strongly associated with ‘clinton’ than it is with any other word tested. 

Additionally, in the same three out of four corpora, the word is more strongly associated with ‘liberal’ than ‘conservative’.

Whether these groups directly used this word as a pejorative descriptor, or merely described its use, its association here across the political spectrum speaks to the centrality of the concept to the current political atmosphere. 

Note: the word has been reclaimed by some groups, and as such it’s possible that within the left-leaning/feminist corpora it is used as a positive, rather than pejorative, descriptor. Nevertheless, it retains its gendered associations, as reflected in the models.

*‘establishment’, ‘soros’*

The words ‘establishment’ and ‘soros’ (the latter being the last name of noted leftist philanthropist George Soros) are terms I would deem conspiracy-related, due to their association with the anti-globalist right. ‘Establishment’ appears in three subreddits: intuitively, r/The_Donald and r/KotakuInAction both contain the term; less obviously, the term also appears in leftist r/esist. 

I would take this opportunity to note that r/esist, while left-leaning, is not explicitly pro-Clinton; in fact there is a sizeable membership of Sanders supporters who view themselves--and Sanders--as explicitly “anti-establishment”. 

Clinton, to many of these contributors, likely represents “the establishment”. And indeed, in all three corpora, ‘clinton’ is more closely related to ‘establishment’ than is ‘trump’. In fact, in both r/KotakuInAction and r/esist, the relationship between ‘trump’ and ‘establishment’ is not just distant, it’s oppositional.

The word ‘soros’ appears in only two subreddits, r/The_Donald, and r/KotakuInAction. In each of these corpora, the models place it much closer to ‘clinton’ than to any other term tested. These results seem to correlate with both the conspiracy-driven aspects of the subreddits 'soros' appears in, and its use as a disparaging indirect reference to Clinton (with anti-semitic overtones, it was frequently suggested that Soros was associated with Clinton in various nefariously-globalist schemes). The word’s modeled proximity to ‘clinton’ mirrors its actual usage in these groups.

*‘prison’, ‘email’, ‘corrupt’*

But what about her emails?

Email played a central role in the 2016 election. Hacked/leaked emails, and a series of accusations of corruption (complete with threats of prison and crowds chanting “lock her up”, the “her” being Clinton) preoccupied media outlets and dogged the Clinton campaign. 

In both the left- and right-leaning corpora, with only the exception of r/feminism, the words ‘prison’, ‘email’, and ‘corrupt’ always appear together. In all five corpora in which it appears, ‘email’ is always closest to ‘trump’.

In all five subreddits in which it appears, ‘corrupt’ is closer to ‘clinton’ than to ‘trump’. And ‘clinton’ is closer to ‘prison’ than either ‘trump’ or ‘sanders’ in all six subreddits tested.

*‘assault’*

Finally, there were several other concepts around which all communities seemed to share a consensus: the word ‘assault’ appeared in every corpus, whether left- or right-leaning. In every case, ‘assault’ was modeled as closer to both ‘trump’ and ‘men’.

__*complete data, including corpora, models, and a jupyter notebook with code for this project is available in [this repo](https://github.com/neurodivergent-ai/WEAT_analysis_1).*__

#### conclusions

Even on tiny corpora, an out-of-the-box word2vec model can find specific cultural relationships--within the limits of the vocabulary--but requires domain knowledge to avoid misinterpreting results. 

In preparing lists of words to compare, it was necessary to take into account whether a given word appeared in the corpus at all. This could be mitigated with a larger vocabulary, which might (but is not guaranteed to) come with a larger corpus. Again, I suspect that the vocabularies of particular subreddits are potentially more limited than those of other collections of similar size, due in large part to the compressed and often repetitive nature of meme-based cultural transmission and internet slang.

Because vocabulary size--more than corpus size--seems to be the limiting factor, cultural domain knowledge is key. Developing a useful testing vocabulary requires some information about the culture being probed in the first place. Vocabulary work-arounds may be necessary to fully explore some concepts. This method increases, rather than decreases, the need for interdisciplinary collaboration among linguists, historians, sociologists, experts in specific languages, and machine learning researchers.

#### what could improve this project?

First, some technical things: 

* I’d like to add more sophisticated mechanisms for comparing term lists. 


* After comparing multiple cosine similarity lists by hand, I think next time I’ll add some scripts to do this for me. 


* Different text preperation methods could affect training & results.


* More exploratory work on the vocabulary could possibly yield better/more complete terms.


* I would also like to add better error handling to the cosine comparison pipeline; currently checking to make sure a word exists in the vocabulary requires sorting through KeyErrors one-by-one, and it can be a hassle if you don’t manually check to see if words are in the vocabulary first. I can fix it, but I was so excited to get this out I rushed that. My bad! If you run this code with your own term lists, I suggest running text prep & model training pipelines separately, training a single model first before running cosine comparisons on lists--unless you already know all the words in your lists are in the vocabulary. 


__Better data__ is on every machine learning wish list. In this case it’s pretty obvious to see how a larger/more complete collection of documents could yield a more robust vocabulary model for exploration. This is intended as a small proof-of-concept only; academic conclusions would require more rigorous research standards.

At the end of the day, every anomaly in this project could be attributed to the small size of the vocabulary--as could any of the relationships that seemed to meet expectations. More testing, on more words (and maybe some better methods) would be needed to say with any certainty. But I think that in this proof-of-concept the corpora are small enough, and the correlations striking enough, to warrant further efforts toward applying similar analyses to more historically & socially significant texts.

More to the point, this project needs __more collaborators__ & __more varying fields of expertise__. *Ok,* you might say, *but that’s true of almost any project*, and you’d be right.

However in my view there’s a special need for caution when using neural nets--of any size or depth--to make inferences about entire cultures. Careful research design (and curation of results) are necessary to minimize the fallout from unexamined biases of those asking the questions. While making inferences about far-right Reddit culture is a fairly low-stakes endeavor--they’re quite upfront about a number of beliefs they hold to be self-defining--scholarship involving historic (or historically marginalized) cultures may have far reaching cultural impact. 

Given our society’s level of technological awareness, adding the perceived authority of “AI” to any scholarly analysis would likely enhance its gravitas in the public mind. This should serve as a caution to researchers: drawing conclusions using technology in isolation from other means of cultural understanding can amplify low-quality scholarship--or worse, project the biases of our society onto populations who, through either extinction or lack of privilege, are not able or allowed to speak for themselves.

Approached with a conscientious, diverse, and inclusive team, training models on historic corpora could yield fascinating results. __So I’d love for linguists, historians, statisticians, etc to weigh in and offer critiques.__

Supposing I could access historic corpora, I have some of the technical skills to build these models--but I lack the interdisciplinary framework to ethically evaluate outside cultures on my own. Tackling this problem ethically requires a team. (Without sounding too grandiose, I would argue that this type of cross-disciplinary collaboration could be powerful medicine for Silicon Valley’s ethics crisis.) I would also appreciate advice from more seasoned natural language processing practitioners. So potential collaborators, please hit me up!

Thanks in advance for your time, and for taking the time to read this.

\***

*This project was originally published on the [Indigenous Engineering blog](https://www.indigenous.engineering/#blog) in 2019. Updated and republished for 2023.*


*Code available [here >>](https://github.com/neurodivergent-ai/WEAT_analysis_1)*

-------


## [*Contact me >>*](https://disesdi.github.io/contact.html)


-------

## References

1. Caliskan, Aylin & Bryson, Joanna & Narayanan, Arvind. (2017). Semantics derived automatically from language corpora contain human-like biases. Science. 356. 183-186. 

-------

[home](https://disesdi.github.io/) | [about](https://disesdi.github.io/about.html) | <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">code</a> | [contact](https://disesdi.github.io/contact.html)
