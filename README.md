# API and Library (App Store Scraper && Mecab)
App Store Scraper is an API which helps users gather information from app stores into one dataframe. The dataset is collected
from lots of reviews on most downloaded/popular apps in South Korea, including kakaotalk, baemin, coupang, naver, etc.
There are 95,874 reviews in total from 11 different applications; the rating scale starts from 1 to 5.

MeCab is an open-source text segmentation library often used to process sentiment analysis with Korean/Japanese sentences.
While words in English are often separated by whitespace or other symbols, lots of Korean words are written without any space
between. Korean tokenization requires reading and recognizing words.
   
# Approach
This project employs two different approaches for sentiment classification:

Recurrent Neural Networks with Bidirectional Long Short-Term Memory (LSTM)
* This approach utilizes LSTM, a special kind of RNN, to classify sequential data in text.
* The LSTM model is trained on the app review to distinguish positive sentiments to negative ones

Support Vector Machine (SVM)
* SVM is a supervised learning model which object is to compute a optimal hyperplane, which
sets boundaries between different classes.
* The model works better for binary classification problems.

# Process
The project goes through the following steps below:

1. Cleansing Data
* Deleted unnecessary columns to reduce the size of datasets
* Converted data into the consistent format and join 11 different datasets in one file.
* Drop rows with null values

2. Eliminating additional rows
* Issues with review datasets: many users have left high ratings with negative comments as they
believe developers/companies focus on those with 4 or 5 ratings on purpose.
--> Deleted half of 5 ratings to lessen the misleading data and boost the accuracies of models
* Inputted 1/5 of dataframe in SVM models due to O(n^2) complexity

3. Building Models
* Initial LSTM Model: training loss < 0.2, validation loss > 0.9
To decrease the significant difference, three solutions were applied:
1. Used oversampling method to adjust imbalanced dataset
2. Increased the number of data from 24,344 to 95,874
3. Placed dropout layers
* SVM Model
To strengthen the SVM model, there were two techniques added:
1. GridSearchSV: Helps finding the optimal parameters that could be used on a model to train
2. K-fold: Divides the original datasets into k subsets with k times iterations to prevent
overfitting

4. Visualization
* Provided confusion matrix to show the percentage of true positive and true negative. 
* Displayed important information, including training/validation loss and ROC in line graphs. 
