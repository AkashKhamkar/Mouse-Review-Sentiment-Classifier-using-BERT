<h1>What is BERT?</h1>

BERT introduced in [this paper](https://arxiv.org/abs/1810.04805 ) 
stands for Bidirectional Encoder Representations from Transformers. If you don't know what most of that means - you've come to the right place! Let's unpack the main ideas:

* <h3>Bidirectional</h3> - to understand the text you're looking you'll have to look back (at the previous words) and forward (at the next words)
* <h3>Transformers</h3> - The Attention Is All You Need paper presented the Transformer model. The Transformer reads entire sequences of tokens at once. In a sense, the model is non-directional, while LSTMs read sequentially (left-to-right or right-to-left). The attention mechanism allows for learning contextual relations between words (e.g. his in a sentence refers to Jim).
* <h3>(Pre-trained)</h3> contextualized word embeddings - The ELMO paper introduced a way to encode words based on their meaning/context. Nails has multiple meanings - fingernails and metal nails.
BERT was trained by masking 15% of the tokens with the goal to guess them. An additional objective was to predict the next sentence. Let's look at examples of these tasks:

<h2>Masked Language Modeling (Masked LM)</h2>
The objective of this task is to guess the masked tokens. Let's look at an example, and try to not make it harder than it has to be:

That's [mask] she [mask] -> That's what she said

<h2>Next Sentence Prediction (NSP)</h2>
Given a pair of two sentences, the task is to say whether or not the second follows the first (binary classification). Let's continue with the example:

Input = [CLS] That's [mask] she [mask]. [SEP] Hahaha, nice! [SEP]

Label = IsNext

Input = [CLS] That's [mask] she [mask]. [SEP] Dwight, you ignorant [mask]! [SEP]

Label = NotNext

The training corpus was comprised of two entries: Toronto Book Corpus (800M words) and English Wikipedia (2,500M words). While the original Transformer has an encoder (for reading the input) and a decoder (that makes the prediction), BERT uses only the decoder.

BERT is simply a pre-trained stack of Transformer Encoders. How many Encoders? We have two versions - with 12 (BERT base) and 24 (BERT Large).

<h2>Is This Thing Useful in Practice?</h2>
The BERT paper was released along with the source code and pre-trained models.

The best part is that you can do Transfer Learning (thanks to the ideas from OpenAI Transformer) with BERT for many NLP tasks - Classification, Question Answering, Entity Recognition, etc. You can train with small amounts of data and achieve great performance!

<h2>Gameplan</h2>
I haved used BERT-BASE-CASED pre-trained model for this project the main reason for going with the base-case model was that words written in uppercase will have more severity
and will complicate the process of classification. Also after loading the dataset I have cleaned it as it contianed some NAN values and and extra column which was not needed. 
For tokenization I used BertTokenizer.from_pretrained for 'bert-base-cased'. after doing the necessary data prep and training the model below are few outputs obtained.

<h2> Outputs obtained from the model on few examples from test data : </h2>

 ![image](https://user-images.githubusercontent.com/34622497/154799044-c08a2c68-a525-447d-8c16-f39dd5394c8d.png)


 ![image](https://user-images.githubusercontent.com/34622497/154799070-5481e7d1-c65e-4228-a67e-9cb841820bd8.png)


<h2> Output of model classifying on raw input text:</h2>

![image](https://user-images.githubusercontent.com/34622497/154798806-89e3c2e1-cf64-4c5a-a7ca-b11e9042e9ed.png)

