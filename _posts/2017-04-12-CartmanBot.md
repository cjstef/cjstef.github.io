### In this post: 
* introduction to [chatbots](https://en.wikipedia.org/wiki/Chatbot)
* applying [markov chains](https://en.wikipedia.org/wiki/Markov_chain) for modeling stochastic processes
* exploring the capabilities of neural networks with Google's [Word2Vec](https://en.wikipedia.org/wiki/Word2vec)

My fourth project at Metis proved to be my favorite endeavor. Following a week of classroom lectures introducing us to [Natural Language Processing], I began toying with the idea of constructing a chatbot as a fun way of exploring and developing my understanding of the plethora of NLP libraries. 

As it turns out, both text and speech based chatbots are quite popular these days, and are deployed with some regularity in online customer support roles by many larger companies. After doing a bit of research on the subject, I discovered a few things. First, there are several different types of chatbots which each cater to a certain task. The image below provides a nice overview, and the corresponding [blog] offers some more detail.

Second, there seemed to be one big challenge chatbots struggled to overcome: emulating a human personality. I set out to develop mine with the intention of tackling this problem, and also the secondary goal of generating new responses (as opposed to explicitly programmed ones) whilst also maintaining some semblence of grammatical structure.

### CartmanBot is Born

After a little deliberation, I settled on modeling my bot's personality after the character Eric Cartman from the popular Comedy Central show South Park. Aside from me being a diehard fan of the show (I've seen all 240+ episodes at least three times), it was also a practical decision to address the first project goal. As anyone who is familiar with the show will tell you, Cartman has about as strong of a personality as any fictional character in existence. 

The dataset I had for training consisted of approximately 72,000 lines of dialogue spanning eighteen seasons of the show. Of those lines, approximately 12%, or 130,000 words, were spoken by Cartman. 

I decided to try two distinct approaches to build a generative chatbot:
1. A probabilistic model based on markov chains (which I was familiar with from undergrad coursework)
2. A Long-Short Term Memory (LSTM) Recurrent Neural Network model built on top of Google's Seq2Seq and Word2Vec libraries in tensorflow (a completely new domain for me)

### Markov Chain Approach

For those not familiar with Markov Chains, they are essentially a probabilistic model for describing a sequence of events where the probability of the future 'state' is dependent only on the present state. <sup>[1]</sup> 

Imagine we are trying to predict the next day's weather, and the options (states) are cloudy, rainy, or sunny. We aren't really concerned with what the weather was like last month, last week, or even yesterday. All that matters is what the weather is like today, because that gives us some information about the likelihood of what it will be tomorrow.

The diagram below depicts the 'state space', which defines the transition probabilities between the states of our markov chain.

[image of markov chain]

Markov Chains have many useful applications, and proved to be a good candidate for a baseline approach to create CartmanBot 1.0.

I began by looking for a markov chain library in python, and stumbled across [pymarkov](https://pypi.python.org/pypi/PyMarkov). I found that, while the library is certainly useful for beginners looking to implement markov chains quickly, it wasn't quite flexible enough to handle the modified structure I had in mind with states being represented by [n-grams](https://en.wikipedia.org/wiki/N-gram) derived from the corpus of Cartman's dialogue text. So I decided to implement my own via python dictionaries.

The code snippet below provides a simplistic example of how the final product worked. Note that the values for each dictionary key are 'weighted' in the sense that certain words appear more often in the list of values, and thus reflect transition states with higher probabilities relative to the other words in the list.

[code snip]

The code for the actual model looks very similar, except that instead of singular words I used a [bi-grams](https://en.wikipedia.org/wiki/Bigram) approach with the help of the [NLTK](http://www.nltk.org/book/ch01.html) library. Each unique word in the dataset of 130k total words was stored as a dictionary key, and the corresponding values were appended as word-pairs that followed the unique key word at any point in the corpus of text.

The result was a surprisingly coherent bot that certainly captured the essence of Cartman:

[cartmanbot image]

### LSTM Approach with Word2Vec and Doc2Vec

At this point in the project, I was satisfied with the results, but had some time left and wanted to take things to the next level. I began exploring the capabilities of [LSTM recurrent neural networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/).

LSTM's are a significantly more complex approach <sup>[2]</sup>, and as with all neural networks, they require a TON of training data to be effective. However the upside is that they are much more robust, and are much more adept at capturing the plethora of nuances in natural language. 

I wanted to implement a conversational component to compliment the generative gibberish CartmanBot was currently limited to. The plan I developed was as such:

#### Using [Doc2Vec](https://deeplearning4j.org/doc2vec)

1. Embed each line immediately preceding a line spoken by Cartman from the dialogue corpus as a vector representing the aggregate scores of the words in that line
2. Allow the user to input a phrase or ask a question and convert to another vector the same way
3. Perform a cosine similarity search to find the most similar vector from the dialogue vector space to the user input vector
4. Fetch and respond with the corresponding line from Cartman that followed the dialogue line

It seemed like a straightforward approach, but proved anything but. To begin with, Doc2Vec is designed with a specific purpose of associating words with labels or labels with words, but not labels with labels. Essentially, it wasn't well suited to make associations between sentences, as I had hoped. On top of that, it only accepts a very specific input format for your text that took some serious debugging to import and actually run the model without error.

While I ultimately did get it to run correctly, its effectiveness was limited by the size of my dataset, an implementation goal not aligned with its designated purpose, and a lack of time to work out the kinks.

### Summary
This project was a great introduction to the awesome capabilities (and occasional headaches) associated with NLP. Though I am a bit disappointed I fell short of my second goal, I got pretty close, and am certainly considering revisiting the problem in the future. 

You can find the jupyter notebook with my code for CartmanBot [here](https://github.com/cjstef/MetisProjects/blob/master/Proj4.ipynb)

[1] Some great additional reading on markov chains [resource](http://setosa.io/ev/markov-chains/) 

[2] More info on [LTSM's](http://lauragelston.ghost.io/speakeasy-pt2/0) and their applications for chatbots



