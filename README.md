# Language-Detection-using-LSTM

Problem Statement:
We have corpus for text in different languages. We are given a test string and we need to find the language of the given string.

Approach:
I plan to use LSTM models for the purpose. LSTMs are very good at generating text given some seed. They generate text character by character. We predict the character by finding out probability for each of the characters after a sequence and predict the character which has the highest probability to occur after a given sequence.

We designed 2 LSTM for English and French language with 128 nodes and trained it with corresponding corpus. We divided corpus into 80-20 train test set. The training set was formed using 40 sequence of characters from corpus and 1 following character. The step size means that we skip that many characters for picking up next sentence for test or train sets We have used stepsize of 1 for training corpus and step size of 20 for test. This helps in getting greater number of training sets The trained neural network could predict probabilities of each character given previous 40 characters(seed). We selected 100 5-character strings from test set randomly to form our test strings and then tried to find out Pr(string|french) and Pr(string|english) and assign a string to that class which has higher probability. We tried many different ways to find out the probability Pr(string|model). Our models needs a seed of 40 character to predict the probability of next character. So, we used the 40 characters preceding the test string in the corpus as our seed for finding prediction probability of first character of the string. Similarily, we use last 39 characters and the first character of sting for finding prediction probability of second character of the string and so on. We multiply these probabilities to get final values of probability Pr(string|model).

Result :
We ran it for 20 epochs and obtained ROC-Auc value of 0.95 and accuracy value of 84% Confusion matrix: [[81 19] [13 87]]

Remember that from epoch to next epoch down to 20 epochs, there should be a decreasing trend of loss value and increase in accuracy value gradually. If there is no gradual increase in accuracy and if it is remaining almost the same then we can depict that your LSTM network is not trained but not that your network is overfitting the data.

Solution for that is to change the learning rate(lr) may be try to decrease the lr value and fit the data. 
Other thing that can be done is to increase the memory units of your LSTM network's hidden layer. If that is not helping you alot then try to increase the layers of your network. Repeat this step until there is gradual increase in accuracy values and gradual decrease in loss values.

Background:
Firstly let me explain the difference between Recurrent Neural Network (RNN) and Long Short Term Memory (LSTM) Networks.
Humans don’t start their thinking from scratch every second. As you read this essay, you understand each word based on your understanding of previous words. You don’t throw everything away and start thinking from scratch again. Your thoughts have persistence.
There have been incredible success applying RNNs to a variety of problems: speech recognition, language modeling, translation, image captioning… The list goes on.

RNN:
Sometimes, we only need to look at recent information to perform the present task. For example, consider a language model trying to predict the next word based on the previous ones. If we are trying to predict the last word in “the clouds are in the 'sky'.” we don’t need any further context – it’s pretty obvious the next word is going to be sky. In such cases, where the gap between the relevant information and the place that it’s needed is small, RNNs can learn to use the past information.

LSTM:
But there are also cases where we need more context. Consider trying to predict the last word in the text “I grew up in France… I speak fluent 'French'.” Recent information suggests that the next word is probably the name of a language, but if we want to narrow down which language, we need the context of France, from further back. It’s entirely possible for the gap between the relevant information and the point where it is needed to become very large.
