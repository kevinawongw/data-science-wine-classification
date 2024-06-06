# Wine Classification

Our main goal was to create a model that uses A-Priori and item
baskets to categorize wine types based on their descriptions. To evaluate the
model, we aimed to create a confusion matrix and evaluate it on how accurately it
predicted a wine variety given a description. We successfully accomplished our
goal of creating the model and the confusion matrix, though we did not achieve
the goal of getting 80% accuracy. We found that many wines were misclassified
when their descriptions did not include any “frequent words” associated with their
wine type. Similarly, there were some words that very commonly appeared in
multiple wine types. To improve the accuracy, we tried things like adding more
words to ignore when looking at descriptions, tweaking the parameters (such as
the threshold to determine what words are considered “frequent”), and ensuring
that each wine type has the same number of data samples. This helped the
accuracy improve, allowing us to a 60% accuracy.
![image](https://github.com/yugo9081/wine-classification/assets/54964332/b214965f-adf7-4f9f-aa98-a536a94bfa8a)

Outside of our original goals, we were able to include a feature that allows us to
generate wine recommendations based on a user input of the flavors, notes and
profiles they were looking for in a wine.

<strong>Techniques</strong>

* Data Wrangling & Text Processing.
  
Our original database was very large, containing over 150,000 entries and
over 600 wine varieties. For the scope of this project, we also needed to
simplify our database to only include the relevant columns: wine_variety
and description). After filtering out unnecessary columns, we also needed
to clean the text of the descriptions and drop non-null. We used the NLTK
library to process our large number of wine description paragraphs by
dividing them into smaller word tokens. We also converted the text to
lowercase and removed all non-descriptive words. Propositions, articles,
and other commonly used words were removed from the descriptions.
Keeping common words in the descriptions would skew the results of the
item basket analysis.

With such a large amount of wine varieties, we also decided to limit the
number of wine varieties to the top six most frequent wines seen in our
dataset. With the top six most common wine varieties, we are still left with
a large amount of entries for each of the six wine varieties to run an item
basket analysis on. If we had chosen to analyze all 633 wine varieties, the
less common wins would only have a few entries to work with.
While evaluating the model, we noticed that wines were often
misclassified as the wine with the most number of samples in our data.
This is because with more samples, the item basket would end up having
more words. This made the variety with the most rows have the most
words in their basket. Similarly, the variety with the least amount of rows
had the fewest number of items in its item basket. To mitigate, we decided
to make all varieties have the same number of data samples. We did this
by choosing the number of samples that the fewest variety had and making
all other varieties have that same number of samples. We decided which
rows to keep by randomly selecting.

* Item Basket Analysis

Item Basket Analysis is a technique that is used to determine what is
frequently seen together. We chose to use Item Basket Analysis because
we were interested in seeing whether certain wine varieties tend to have
similar profiles thus possibly yielding common wordsets within each type
of wine. In our implementation, we converted our description into an array
of words. Doing so allowed us to use Itertools to quickly generate all
possible combinations.

* A-priori Algorithm
  
Along with the Item Basket Analysis, we used A-priori Algorithm to mine
frequent itemsets. In this algorithm, we computed the ‘support’ by
counting the number of entries an item/itemset appears. We then computed
the ‘confidence’ by dividing it by the total number of entries. When the
confidence meets the threshold, we consider the item/itemset frequent.
Our decided threshold was 0.015. Since threshold can vary significantly
based on the project and what the dataset looks like, there was not a clear
guide on how to pick the best threshold. Therefore, we chose several
different thresholds and chose the best performing one.

* Confusion Matrix
  
To evaluate our model at the end, we used the confusion matrix to check
how accurate it predicts the wine variety based on the description and have
summarized our results. To approach this, we iterated through each of the
predicted labels and plotted it on which label it was predicted to be and
which label it actually was. We also displayed the accuracy, which was
calculated by <img src="https://github.com/yugo9081/wine-classification/assets/54964332/1552477e-b4a3-4fa4-8c0c-3526c99573d7" width="180">. We used the seaborn python library to display the confusion matrix like a heat map.
