# Opinion Piece Generator

A machine learning model which writes opinion pieces based on the style of an author.

![](https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Media/generating_tweet.gif)



## What it does

The Opinion Piece Generator generates a rough draft of an opinion piece based on the style one or various texts. 

[Image]

In addition, fragments of the opinion piece could be used as a basis for, say, social media content or marketing materials:

[Image]

The repository also includes metrics and visualizations to see how well the Generator imitates the style of the original texts:

[Image]



## Usage

### Pipeline

The data pipeline involves several steps:

![](https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Media/pipeline_diagram.png)

#### Scraping 

#### Cleaning

#### Analyzing

#### Modeling

#### Generating

We used a Neural Network LSTM and trained it with over 1000 epochs.



## Dataset

The dataset with all the scraped and cleaned articles from the authors (Denisse Dresser, Enrique Krauze, John Ackerman, Ricardo Raphael, and Valeria Moy) can be found in the /Data/Data_clean_csv directory.

| Dataset  | Location                                                     | Date of scraping |
| -------- | ------------------------------------------------------------ | ---------------- |
| Articles | https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Data/Data_clean_csv/clean_dataframe.csv | 91-03-2021       |