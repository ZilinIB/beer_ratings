# beer_ratings
Source code for kaggle competition 'beer ratings'

## Data fields

  * index - an identifier for the review
  * beer/ABV - the alcohol by volume of the beer
  * beer/beerId - a unique ID indicating the beer reviewed
  * beer/brewerId - a unique ID indicating the brewery
  * beer/name - name of the beer
  * beer/style
  * review/appearance - rating of the beer's appearance (1.0 to 5.0)
  * review/aroma - rating of the beer's aroma (1.0 to 5.0)
  * review/overall - rating of the beer overall (1.0 to 5.0)
  * review/palate - rating of the beer's palate (1.0 to 5.0)
  * review/taste - rating of the beer's taste (1.0 to 5.0)
  * review/text - the text of the review
  * review/timeStruct - a dict specifying when the review was submitted
  * review/timeUnix
  * user/ageInSeconds - age of the user in seconds
  * user/birthdayRaw
  * user/birthdayUnix
  * user/gender - gender of the user (if specified)
  * user/profileName - profile name of the user

## Analysis
Among the above columns:

The following columns shouldn't be included in the feature set, reasons are given for each:
  * review/appearance, review/aroma, review/overall, review/palate, review/taste: the target ones that we want to predict   for the test dataset. 
  * beer/name: redundant to beer/beerId
  * review/timeStruct: redundant to review/timeUnix
  * user/birthdayRaw, user/birthdayUnix: redundant to user/ageInSeconds

The other columns can be used as features and we could divide them into three groups
  1. Numerical features:
    * beer/ABV, review/timeUnix, user/ageInSeconds
    The easiest to deal with, we could normalize them and feed them to the NN directly
  2. Categorical features:
    * beer/beerId, beer/brewerId, beer/style, user/profileName, user/gender
  3. Text feature:
    * review/text
    
## Strategy
The numerical features are the easiest to deal with, we could simply standarize them and then feed to the neural network as input. Note that some entries in the user/ageInSeconds column is missing, we could deal with it by filling the empty entries with average age.

Categorical features are more troublesome. The first idea is to use label encoding. For some features that might work but for some features such that test dataset contains categories that are not seen in the training set, it doesn't work. Then we might considering using one hot encoding and set those unknown categories to 0. However, for features that has massive amount of unique values, the sparsity nature of one hot encoding will produce too many dimensions, which is clearly infeasible. Lastly I come to the idea of using entity embeddings to transform the categories into low-dimensional vectors in some euclidean space. And then feed them to the neural network.

The remaining text feature is the hardest to handle. With different methods one might get completely different results. Therefore I create a baseline model that only uses the numerical features and the categorical features for comparison.

For the final model I used words embedding for sentiment analysis. First I clean up the text by lowering case and removing all special characters etc. Then I transform each review text to a fixed length of integer sequence by keras' tokenizer and zero padding (truncation when the length exceeds). So that I can feed them to a embedding model and take the output as the additional input for the baseline model.

## Result
The baseline model achieved 0.55355, 0.55662 (private/public score)
The final model achieved 
