# Opinion Piece Generator

An neural network which writes opinion pieces based on recent news and the style of an author.

![](https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Media/newspaper_cover.JPG)

NOTE: Although all the examples shown in this file are in Spanish, the model can be used for any language.



## What it does

The Opinion Piece Generator generates a rough draft of an opinion piece based on the style of one or various texts:

> El día pasado entre el segundo debate se encuentra en estas agencias que se enredó de acuerdo al INE. El alumno no es menor, pero en vez de invertir ninguno de sus términos en nuestro país. Pero es un gobierno en otro momento, cuando está de acuerdo. Los militares no son las propuestas ni lograrán crecimiento que nunca podemos predecir o ver las divisas en la mayoría de la sociedad. Ahora bien, el INE se decidió, la libertad y un 20% de la población más alta del país hoy que le volvió al expresidente de la del Superior de la Constitución. En su vez, el Estado de medicamentos en 2017 del viejo régimen de oprobio y a medio de un comportamiento de una semana de las personas estadounidenses, en otros ámbitos de la vida para el Instituto Nacional de Normalización y venta del Banco de la Revolución Pública, hacen de favor del partido. Pero es el que hoy ha hecho un acompañamiento heroico del artículo de Andrés Manuel López Obrador para su presidencia...
>

<br/>

Fragments of the generated text could then be used for social media content or other marketing materials: 

![](https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Media/dashboard_tweets.png)

<br/>

Finally, the project includes metrics and visualizations to see how well the Generator imitates the style of the original texts. The following is a dashboard based on the articles of the Mexican columnist Denisse Dresser:

![](https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Media/dresser_dashboard.JPG)

<!--Dashboard of Denisse Dresser-->

All these result are compiled in a presentation:

- [English version](https://docs.google.com/presentation/d/e/2PACX-1vTVM4TPNa6OdZ22WhfMQQ8K26xxAOX9WyWd9dg_BNS7Ewpo8hNM-mOuUOH-1GlZKNCRDnO4kMbf6ukK/pub?start=false&loop=false&delayms=3000)
- [Spanish version](https://docs.google.com/presentation/d/e/2PACX-1vRMJXoboPJakyBzyhlO3Myci905Xl9RMtz5xU1tDwADMYl0jUtkbl3oK_k1aBAtPsm5F6EI3dezyBko/pub?start=false&loop=false&delayms=3000)

## How it is built

To create the  generator, we followed five steps:

![](https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Media/pipeline_diagram.JPG)

To demonstrate, we selected the articles of five prominent Mexican columnists: 

- Denisse Dresser
- Enrique Krauze
- John Ackerman
- Ricardo Raphael
- Valeria Moy

### Scraping 

We used [Selenium](https://selenium-python.readthedocs.io/) to extract all the links to the articles the authors, either from their personal website or a news & media website. Then, we extracted the body of the articles with [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/).

Here's a [**Notebook Example**](https://nbviewer.jupyter.org/github/FranciscoGalan/Opinion_Piece_Generator/blob/main/Scraping/scraper_Enrique_Krauze.ipynb) for the articles of author Enrique Krauze.

The rest of the scrapers can be found in the /Scraping directory and the raw data is located in Data/Data_raw. 

### Cleaning

We removed the html tags from the articles using RegEx, formatted the dates, and joined the information in a DataFrame. 

The notebook **[Cleaner_main.ipybn]()** contains all the cleaning functions:

- `date_cleaning`: Transforms all scraped dates to the format YYYY/MM/DD.
- `html_cleaner`: Cleans all html expressions.

The dataset with all the scraped and cleaned articles from the authors can be found in the /Data/Data_clean_csv directory:

| Dataset  | Location                                                     | Date of scraping |
| -------- | ------------------------------------------------------------ | ---------------- |
| Articles | https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Data/Data_clean_csv/mixed_dataframe.csv | 91-03-2021       |

### Analyzing

We wrote several functions to calculate the clarity metrics of a text (see **[Notebook](https://nbviewer.jupyter.org/github/FranciscoGalan/Opinion_Piece_Generator/blob/main/Text%20Analytics/Clarity%20metrics.ipynb)**):

- `avg_word_per_sentence(text)`: Returns average words per sentence of a text.
- `avg_syllables_per_word(text)`: Returns average syllables per word of a text. It uses the [textstat](https://pypi.org/project/textstat/) library to count the syllables of a word.
- `szigriszt_pazos_adapted(text)`: Returns the readability index of a text. It uses [textstat](https://pypi.org/project/textstat/) to calculate the [szigriszt-pazos index](https://legible.es/blog/perspicuidad-szigriszt-pazos/). 
- `word_frequency_score()`: Returns a score of how frequent are the words used in the text. It uses the [wordfreq](https://pypi.org/project/wordfreq/) library. 

The word clouds were generated with a png image of the authors and [wordcloud](https://pypi.org/project/wordcloud/) (see **[Notebook](https://nbviewer.jupyter.org/github/FranciscoGalan/Opinion_Piece_Generator/blob/main/Text%20Analytics/WordCloud%20generator.ipynb)**).

![](https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Media/wordclouds.JPG)

### Modeling

This **[Notebook](https://nbviewer.jupyter.org/github/FranciscoGalan/Opinion_Piece_Generator/blob/main/Models/Notebooks/Model_generation_training.ipynb)** contains all the following steps in the modeling process. 

#### Data preparation

To prepare the text data for our model, we  

1. formatted it with the `clean_text` function;
2. tokenized it with Keras's `Tokenizer` (that is, assigned a different numeric value to each word);
3. created token sequences with `generate_sequences` function, which returns a series of X values (word-sequences of n length) and y values (the next word for a corresponding X sequence), and 
4. converted our X and y values to np.arrays to train our model. 

#### Model characteristics

We have an input layer which which receives a word sequence of size 20. Also, we have an embedding layer of size 100, which holds the weights learned for each word in our tokenizer object.

We decided to use Long Short Term Memory layers, a kind of Recurrent Neural Networks with can predict values based on sequences even a hundred steps long. We used four LSTM layers with Drop Out layers in between to avoid overfitting.

Finally, we used a dense layer with a softmax activation, and compiled our model with an Adam optimizer and a cross entropy loss function.

#### Model training

Considering the limited processing power of our computers, we did multiple rounds of training with 200 epochs per round and a checkpoint function to our callbacks. In this way, we could save our model every time it improved its loss score and re-load it. Also, we generated and printed random text after each epoch to see how well it was going. 

We saved the model after 1000 epochs, since, after that point, the model did not improve its score.

### Generating

We use the Twitter API to extract a seed for our model. In this way, the model generates text about the most recent or trending news in Twitter.

Then, our [fake Twitter account](https://twitter.com/IhLstm) posts fragments of the generated text (see [Notebook](https://nbviewer.jupyter.org/github/FranciscoGalan/Opinion_Piece_Generator/blob/main/Twitter_post/Twitter_Reforma.ipynb)).

