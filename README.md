# Transformer Translation

This is a pytorch implementation of the transformer model，which is actually a modified version of  https://github.com/SamLynnEvans/Transformer. Thanks for the author of this source project.

# Usage

Two text files containing parallel sentences (seperated by '\n' characters) in two languages are required to train the model. See an example of this in the data/ folder (french.txt and english.txt).

To begin training, run this code:
```
python train.py -src_data path/lang1.txt -trg_data path/lang2.txt -src_lang lang1 -trg_lang lang2
```
The spacy tokenizer is used to tokenize the text, hence only languages supported by spacy are supported by this program. The languages supported by Spacy and their codes are:

English : 'en'<br />
French : 'fr'<br />
Portugese : 'pt'<br />
Italian : 'it'<br />
Dutch : 'nl'<br />
Spanish : 'es'<br />
German : 'de'<br />

For example, to train tan English->French translator on the datasets provided in the data folder, you would run the following:
```
python train.py -src_data data/english.txt -trg_data data/french.txt -src_lang en_core_web_sm  -trg_lang fr_core_news_sm  -epochs 10
```
Additional parameters:<br />
-epochs : how many epochs to train data for (default=2)<br />
-batch_size : measured as number of tokens fed to model in each iteration (default=1500)<br />
-n_layers : how many layers to have in Transformer model (default=6)<br />
-heads : how many heads to split into for multi-headed attention (default=8)<br />
-no_cuda : adding this will disable cuda, and run model on cpu<br />
-SGDR : adding this will implement stochastic gradient descent with restarts, using cosine annealing<br />
-d_model : dimension of embedding vector and layers (default=512)<br />
-dropout' : decide how big dropout will be (default=0.1)<br />
-printevery : how many iterations run before printing (default=100)<br />
-lr : learning rate (default=0.0001)<br />
-load_weights : if loading pretrained weights, put path to folder where previous weights and pickles were saved <br />
-max_strlen : sentenced with more words will not be included in dataset (default=80)<br />-max_strlen : sentenced with more words will not be included in dataset (default=80)<br />-checkpoint : enter a number of minutes. Model's weights will then be saved every this many minutes to folder 'weights/'<br />

# Training and Translating

```
python train.py -src_data data/english.txt -trg_data data/french.txt -src_lang en_core_web_sm  -trg_lang fr_core_news_sm  -epochs 10
```
This code gave the following results on a GeForce Nvidia 3060 GPU:

After saving the results to folder 'weights', the model can then be tested:
```
python translate.py -load_weights weights -src_lang en_core_web_sm  -trg_lang fr_core_news_sm
```

So with a small dataset of 150,000 sentences and 1 hour of training, already some quite good results...

# Features still to add

- create validation set and get validation scores each epoch
- function to show translations of sentences from training and validation sets
