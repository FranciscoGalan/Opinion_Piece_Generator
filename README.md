# Opinion Piece Generator

A machine learning model which writes opinion pieces based on the style of an author.

![](https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Media/generating_tweet.gif)

NOTE: Although all the examples shown in this file are in Spanish, the model can be used for any language.

## What it does

The Opinion Piece Generator generates a rough draft of an opinion piece based on the style one or various texts. 

[Image]

Fragments of the opinion piece could also be used for social media content or other marketing materials:

[Image]

Finally, the repository includes metrics and visualizations to see how well the Generator imitates the style of the original texts:

![](https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Media/dresser_dashboard.JPG)



## How it is built

To create the  generator, we followed these steps:

![](https://github.com/FranciscoGalan/Opinion_Piece_Generator/blob/main/Media/pipeline_diagram.png)

To demonstrate, we selected five famous Mexican columnists (Denisse Dresser, Enrique Krauze, John Ackerman, Ricardo Raphael, and Valeria Moy) and used their articles as a basis.

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