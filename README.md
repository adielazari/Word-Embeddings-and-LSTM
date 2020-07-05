### Word-Embeddings-and-LSTM

#### Data Preprocess and exploratory
The dataset contains a description of a product, a search line, and how much of the search line is relevant to the product. Our goal in this project is to try to predict the product search line relevance given a description of a product and a search line.
In order to clear the data we made stemming(Porter) and we downloaded stopwords for product title and search term.

#### Characters and words  based  Siamese networks
One of the greatest difficulties we faced was to understand from the article what we need to do and what they intended when they intended for a Siamese model and how it can be used for our purpose.
Finally we realized that the goal of the Siamese model is to get 2 different inputs  to run on each of them  lstm  and finally provide a single output  that will give therelevance  between the 2 inputs.
To perform preprocess the  process We performed tokenizing  to Letters  (in part A) and to the words (in part B), and then we converted it tosequence  and limited the sizeofsequence  to 300  (in part A) and to the maximum values of thetokens  (in part B)  . So the end for each  product Titl\setarch term  receives an array that contains  sequence of the size  defined  by the letters  or words  and the amount of occurrences that appear in each one.
Another difficulty we encountered is the problem that after receiving thesequence  for each of the values, it wasthat theinput thatlstm  accepts differs from what we accept (lacking  the time dimension) and so we had to perform  reshape  toinput  (what we should not have done for thewords  because they are made  embedding before the lstm). 
Finally building the model because we have two different Lstm  for theproduct title  and one for thesearch term  we had to connect between the weights of both, to do this in a way that will give the best results we have made some interconnectitio  But finally the model that gave the best results is a model made separately for addition, subtraction and outputs for the 2outputs  and finally to connect the results we committed  concatenate  on the three results we received  from the connection, subtraction  and a fold.

Because at the end ofour output  is one of our last layers  , you werethe dense layer (with the  relu acbatdo ) provided by a single output  .
Finally, we usedAdam  asoptimizer  and  Rmse  as theLOSSfunction.

Because at the end of our output is one of our last layers, you were the dense layer (with the  relu acbatdo ) provided by a single output  .
Finally, we used Adam  asoptimizer  and  MAE  as the LOSS function.

#### Naïve Linear Regression
To provide a model benchmark  that we can compare our results to which we have decided to use the linear regressionmodel. Because it is a naïve model, we have decided to integratetheproduct  title  and thesearch term  to a single input, the model will classifytherelevance  Given the letters  and their number of occurrences in both values. After the combination we have created  pipeline  that the count Vectorizer  performs (getting an array of the letters  that appear intheinput  and the amount of occurrences), and then whatoutput  oftheVectorizer  brings into the model  linear regression. input
We trained the model and examined the results below:
 
#### LSTM as feature extractor
The third part of our performance is making learning transfer  that means usingthe output  ofthelstm model  asfeature extraction  to the  MLmodel. The models we decided to use are  xgboost models and because itis aregression(a numerical value and not a catechism( we used the KNN_regression model , theinput  of the  preceding D.ense models (conc_layer  ). In this part, too, we have been very difficult to use theoutput of the Siamese model  so that it fits theML INPUT  (which took us a long time).


•	We finally made a graph comparing the four models we built
Between  chracters  based models:
![image](https://user-images.githubusercontent.com/44158047/86533010-beb47e00-bed6-11ea-8d8f-eb044d02703f.png)

 
And words based models:
 
The parameters on which theshow is compared  aretheRmse, the training time, and the time of prediction.
You can see that the least good model today the Siamese model and the והKNN  which in the Siamese model time workout was a significant big one from the rest of the time and theKNN was the most significant of the rest and for both theRmse  was the highest.


To summarize the ratio between the character level  model andword level with  thisembedding wordlevel in the training time and the network's test is growing very much and it is because of theembedding, but gives better results besides the fact that it is more over  fitting than the  character level model. Conversely, thefeature extraction for the  xgb  andKNN models while reduced in  word level  that has fewer  tokens  but did not change the indices.

