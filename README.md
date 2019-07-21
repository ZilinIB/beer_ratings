# beer_ratings
Source code for kaggle competition 'beer ratings'

## Data fields
*index - an identifier for the review
*beer/ABV - the alcohol by volume of the beer
*beer/beerId - a unique ID indicating the beer reviewed
*beer/brewerId - a unique ID indicating the brewery
*beer/name - name of the beer
*beer/style
*review/appearance - rating of the beer's appearance (1.0 to 5.0)
*review/aroma - rating of the beer's aroma (1.0 to 5.0)
*review/overall - rating of the beer overall (1.0 to 5.0)
*review/palate - rating of the beer's palate (1.0 to 5.0)
*review/taste - rating of the beer's taste (1.0 to 5.0)
*review/text - the text of the review
*review/timeStruct - a dict specifying when the review was submitted
*review/timeUnix
*user/ageInSeconds - age of the user in seconds
*user/birthdayRaw
*user/birthdayUnix
*user/gender - gender of the user (if specified)
*user/profileName - profile name of the user

## Analysis
Among the above columns:

   *review/appearance, review/aroma, review/overall, review/palate, review/taste: the target ones that we want to predict   for the test dataset. 
      
