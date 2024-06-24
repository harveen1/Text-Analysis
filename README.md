Bears and Bulls: Emotional Sentiment Surrounding the Stock Market

This paper explores data surrounding public sentiment around the current state of the market in light of the high inflation rates, bank failures, and a looming recession. The question I am looking to address is, how can public sentiment be used to explain current and future trends in the United States economic market? 

Data Description

The data used for this analysis comes from the social media platform Reddit, specifically the subreddit r/wallstreetbets. There are many different opinions on this page, a lot of which could be considered controversial, making it a great place to source sentiment data.
Using the Reddit API and ‘RedditExtractoR’ package in R, I was able to search r/wallstreetbets for posts from the last month (4/8/2023 – 5/7/2023). The data was not very cohesive so many pre-processing steps were taken to make it suitable for analysis in R. First, I combined the “title” and “text” fields as the majority of fields in the “text” column were blank; users will typically put their entire post in the “title” field or insert an image, which would not be picked up by processing in R. From here, I began labeling posts as either “positive” or “negative.” The classifiers were binary so as to simplify the prediction model. Any posts with clearly negative or positive opinions were labeled accordingly. Posts that mentioned a “bearish” market were also labeled as “negative” while bullish was considered “positive.” Sarcasm and multiple counts of foul language were considered “negative” as well. 
Once the data was labeled and read into R, more pre-processing steps were taken. To make the features as consistent and cohesive as possible, I used commands to remove punctuation, numbers, URLs, separators, and stopwords. I also used a dictionary and used a command to keep all words found in that dictionary to remove many of the nonsensical words. Although the data was not perfect, these measures were quite helpful when the time came for the actual analysis. 

Explanation of Analysis

I chose to use supervised learning methods as the categories for this data had already been determined to be “positive” and “negative,” and we are looking to make predictions based on these categories. Specifically, I tested both Naïve Bayes and Support Vector Machines (SVM) predictions. Although the two methods are similar, I was looking to see if using K-folds would have an effect on the overall accuracy, precision, and recall results. Within this test, I also checked to see if the k value for the K-folds would affect the accuracy and there was a very large discrepancy between k = 5 and k = 10. Ultimately, I went with k = 10 and the SVM model to plug into the prediction model at the end.
I also created a visualization for the most common words which were featured at least 100 times. This helped double check that all stopwords and unnecessary features had been removed as well.   
 

Results

Given how much nuance there is in the Reddit posts when it comes to factors like tone and sarcasm, I considered a prediction model with over 50% accuracy to be successful, although the higher the better. Below, I am including the output of the confusion matrices for the Naïve Bayes prediction model and then the SVM model. Although the accuracy was higher for the Naïve Bayes model, the recall was only at 5 percent. The SVM model had a much better recall with almost 43 percent, but the accuracy was 3 percent lower at about 60% and the precision was about the same. Regardless, both models held up to the standard and had above a 50% accuracy rate.  

Naïve Bayes
Confusion Matrix and Statistics

          Reference
Prediction  negative  positive

  negative       176        97
  
  positive         8         6
                                        
               Accuracy : 0.6341        
                 95% CI : (0.5755, 0.69)
    No Information Rate : 0.6411        
    P-Value [Acc > NIR] : 0.6228        
                                        
                  Kappa : 0.0182        
                                        
 Mcnemar's Test P-Value : <2e-16        
                                        
              Precision : 0.42857       
                 Recall : 0.05825       
                     F1 : 0.10256       
             Prevalence : 0.35889       
         Detection Rate : 0.02091       
   Detection Prevalence : 0.04878       
      Balanced Accuracy : 0.50739       
                                        
       'Positive' Class : positive  



SVM 
Confusion Matrix and Statistics

          Reference
Prediction negative positive

  negative        47        20
  
  positive        21        15
                                          
               Accuracy : 0.6019          
                 95% CI : (0.5008, 0.6971)
    No Information Rate : 0.6602          
    P-Value [Acc > NIR] : 0.9106          
                                          
                  Kappa : 0.1189          
                                          
 Mcnemar's Test P-Value : 1.0000          
                                          
              Precision : 0.4167          
                 Recall : 0.4286          
                     F1 : 0.4225          
             Prevalence : 0.3398          
         Detection Rate : 0.1456          
   Detection Prevalence : 0.3495          
      Balanced Accuracy : 0.5599          
                                          
       'Positive' Class : positive


Findings

Through this process, it was clear how necessary pre-processing was in order to get the best accuracy, precision, and recall rates. This would apply to any social media data as there is no standard language being used, with plenty of differences in spelling, tone, and style. Once the data has been cleaned, the SVM prediction model can be applied to future Reddit (or any social media platform) posts to determine public sentiment. The sentiment can then be compared to trends in the stock market to investigate any potential correlation. 
Looking at the data outside of the model itself, a majority of the posts in r/wallstreetbets were negative. As the market has been going down in recent months and confidence among the public is low with a recession on the rise, this result was expected. If the public opinion continues to be negative, it might mean investors continue to make decisions that are reactive meaning the trends will continue going downward. Using this data and being able to predict overall sentiment can help explain these trends; if posts start leaning positive, it might mean the public has more confidence and it could affect the direction of the market as well.
While considered successful in this case, a 60 percent accuracy rate may not be considered ideal if this model were to be used by other researchers. In that case, I might recommend additional pre-processing steps be applied before running the model, but it is still important to recognize that the model would not be able to pick up on stylistic elements unless a new dictionary was applied.
