
# WeRateDogs Data Wrangling Project

Udacity DAND project on "We Rate Dogs" twitter account data
This project is wrangling the twitter accound data of "We Rate Dogs" and aiming to come up with several insights.
The below are the steps of data wrangling in this project.

<a id='DG'></a>
## Data Gathering

The below information are the used datasets in this project with a details of download method:
1. Enhanced Twitter Archive : Downloaded manually and load programmatically using pd.read_csv and named the dataframe as twitter_archive


2. Image prediction : Downloaded programmatically from [here](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv) used requests library and stored the dataframe as image_prediction


3. JSON Data : Downloaded programmatically from [here](https://s3.amazonaws.com/video.udacity-data.com/topher/2018/November/5be5fb7d_tweet-json/tweet-json.txt) and stored the dataframe as json_tweets

## Assessing Data

This stage is inspecting the dataset visually and programmatically for: 
1. data quality issues
2. lack of tidiness

### Quality Issue:

_Twitter Archive:_
1. Data type: Timestamp datatype should be DateTime not an object
2. Column name: 745 missing value
3. Column name: 109 are non dog name
4. We are only interested with tweet not retweet, only keep columns with NaN for 'retweeted_status_id', 'retweeted_status_user_id' and 'retweeted_status_timestamp'
5. missing value for 'doggo','floofer','pupper','puppo'
6. some rating numerator and rating denominator values are not correct

_Image Prediction:_
7. Dog name in p1, p2, p3 are began with Uppercase sometimes, lowercase other time.
8. Dog name : replace '_' with space
9. 324 prediction data that shows no valid dog from all the prediction (p1,p2,p3)

_JSON Data:_
10. 2354 id data, missing 2 data compared with the twitter_archive


### Tidiness Issue: 

_Twitter Archive:_
1. doggo, floofer, pupper, and puppo can be melt and name the column into "dog_stage"
2. we only interested with original ratings with, hence drop the uneccessary retweet and reply column (retweeted_status_id , retweeted_status_user_id , retweeted_status_timestamp)

_ImagePrediction:_
3. Only keep necessary data such as tweet_id, jpg_url, dog1, dog2, dog3
_JSON Data:_
4. JSON data should be merged with Twitter_archive dataset

## Cleaning Data

### Quality Issue:
In this process, I created a copy for each dataset, which named as tw_clean, image_clean, and j_clean

_Twitter Archive:_
1. Convert Timestamp datatype from object to datetime format

2. Column name:  109 are non dog name and replaced by 'None' by using replace function.

3. only interested with tweet not retweet, thus only keep columns with NaN for 'retweeted_status_id', 'retweeted_status_user_id' and 'retweeted_status_timestamp '

4. missing value for 'doggo','floofer','pupper','puppo' as printed as 'None', replaced with ''

5. Some rating numerator and rating denominator values are not correct, thus I extracting numerator from the text and calculating Rating Ratio by dividing rating_numerator with rating_denominator and we set the rating ratio range from 0-3

_Image Prediction:_
7. We replaced the first letter in Dog name in p1, p2, p3 with uppercase

8. Dog name : replace '_' with space

9. 324 prediction data that shows no valid dog from all the prediction (p1,p2,p3), replaced with 'None' value

### Tidiness Issue: 

_Twitter Archive:_
1. doggo, floofer, pupper, and puppo can be melt and name the column into "phase", and dropped the doggo, floofer, pupper and puppo columns as it has been merged into 'phase'column

2. we only interested with original ratings with, hence drop the uneccessary retweet and reply column (retweeted_status_id , retweeted_status_user_id , retweeted_status_timestamp , in_reply_to_status_id , in_reply_to_user_id)

_ImagePrediction:_
3. Only keep necessary data such as tweet_id, jpg_url, dog1, dog2, dog3, thus I dropped the unnecessary columns

_JSON Data:_
4. JSON data should be merged with Twitter_archive dataset and before merging the dataset, I renamed the 'id' with 'tweet_id' 


For Analysing Purpose, I merged Twitter_archive, Image_prediction, and JSON dataset for ease of data accessibility

After merged the dataset, then I stored it as complete_df

## Insight

- Average rating ration is 1.05 and there is a positive relationship with number of retweet and favorite. Any ration is bigger than 1, the trends will increase exponentially over the number of retweet and favorite

- Based on the above observation, Type of dog breeds that always be in top rating, favorite, and retweet are Golden Retriever, Labrador Retriever, Pembroke, Cihuahua, and followed by Samoyed or Pug (only for rating). Golden Retriever is the most favourite, rated, and retweet dog breed and it has significant difference with other type of dog breeds, as we can refer Labrador Retriever

- Based on Rating Ratio: Doggo, floofer and puppo are most favorite dog stage, Based on Retweet:Doggo is the most favorite dog stage, Based on favorite:puppo is the most favorute dog stage, Pupper is the least favorite among these three analyses

- Based on the observation on above chart, it shows that the optimum time of people engaging in twitter is approximately from 04:00pm - 06:00pm and start to decrease during dinner time (07:00pm - 10:00pm) and it increases significantly to the peak point in the midnight time from 00:00- 01:00am. This would suggest that in order to achieve high retweet and favorite, it's recommended to post the tweet within the above suggested time since there is more people engaging with social media. 


```python

```
