# <span style="color:#2ac965;"> Algorithms Description </span>
## 1) Batch Perceptron Algorithm


#### The perceptron Algorithm is inspired by the biological neural networks (BNN) , where each neuron transmits and recieves various stimulus from all over the body, but there is a condition , ***that this summation stimulus must be over a certian thershold*** to be transmitted to the axon. The perceptron tries to imitate this image in a computational way.

![Perceptron Flow Chart](readme%20images/1.png "Perceptron Flow Chart")

so lets model the perceptron <br>
1. Perceptron models a neuron<br>
2. it receives * N * inputs according to the features <br>
3. it sums those inputs, checks the result and produces an output<br>
4. checks if the input is above a certain thershold or not and behave accordingly, if the input exceed the threhoshld it will output 1 else it will output 0. This compraison is done by a Transformtion Function <br>

> The goal of the preceptron is to Find the Corrects weights that will output correct results <br>

5. The Transfer Function (Activation Function) translates input into output, and the commonly used is the Sigmoid Function<br>
6. Also we add a term called "Bias" to shift the transfer function horizontally <br>
7. The learning rate which controls the changing in both the weights and the bias

>  So to Sum Up, it takes an input which is Training set, aggregates it (weighted sum), and returns 1 only if the aggregated sum is more than some threshold, else returns 0 
>> This Rewrites the threshold and making it a constant input with a variable weight
> u = weights multipled (dot product) by x_training data<br>

- If y_training multiplied by u (both scalars) <= 0 <br>
- change/update delta<br>
- Delta = Delta / size of training data (Averaging)<br>
- Update weights untill we reach an acceptable error percentage

> A key word for the normal Batch perceptron that it uses fixed Training DataSet of fairly small size
---

## 2) Online Training Algorithm

#### They are both pretty similar but the Online Training is used with Large Continous flowing data, On-line learning algorithms take an initial guess model and then picks up one-one observation from the training population and recalibrates the weights on each input parameter.

#### In the online model, you are allowed to make exactly one pass on your data, so these algorithms are typically much faster than their batch learning equivalents, thus deploying online algorithms in production typically requires that you have something constantly passing datapoints to your algorithm.

#### If your data changes and your feature selectors are no longer producing useful output, or if there is major network latency between the servers of your feature selectors, or one of those servers goes down, or really any number of other things, your learner tanks and your output is garbage. 
#### ***Making sure all of this is running ok can be a trial.***

> The main difference between the online and the batch is that the online training processes data piece by piece while the batch perceptron processes the data in batches , hence the name <br>
>
> So to sum up, The online algorithm Takes input which is large continous training dataset(this wasnt applied in our problem), then get:<br> 
>> u = weights multipled (dot product) by x_training data<br>

![Online Flow Chart](readme%20images/online_flow_chart.png "On-line Flow Chart")

- if  y_training multiplied by u (both scalars) <= 0<br>
	- change/update delta<br>
	- Delta = Delta / size of training data (Averaging)<br>
	- Update weights<br>
- Untill we reach an acceptable error we keep iterating<br>

The weight is updated inside the If statment to make the test one by one not as a batch

---

# <span style="color:#2ac965;"> Algorithms Implementation </span>

## 1) Batch Perceptron function

![Batch Function](readme%20images/batch_code.PNG "Batch Algorithm Function")

- The plots array is used to append the norm of deltas while iterating to plot them later against deltas generated from the online function
- The epochs variable is calculated here only for the breaking out of the function in case of too many iteration (Not linearly sperable data)
- other than that the epochs in the batch algorithm is equal to length of weight_steps, so we don't have to return it
---

## 2) Online Training Algorithm

![Online Function](readme%20images/online_code.PNG "On-Line Algorithm Function")

- In the on-line function on the other hand, number of epochs has to be calculated since it isn't equal to length of weight_steps
- I also use it here to break out of the function as well at 1000 iterations 

---

# <span style="color:#2ac965;"> Comparisons from sheet 3</span>

## 1) Problem 1 data

![Problem 1 batch](readme%20images/problem1_batch.PNG "Problem 1 batch: weights changes & Epochs")

- As mentioned before, in the batch algorithms the Epochs is the same as the number of times the weights changed <br><br><br>

![Problem 1 on-line](readme%20images/problem1_online.PNG "Problem 1 On-line: weights changes & Epochs")

- We can clearly see that the number of weights changes here is darastically less than the batch algorithm one
- also the number of epochs is less than the number of weights changes here as expected from the algorithm <br><br><br>

![Problem 1 delta changes](problem1_online_vs_batch.png "Problem 1 delta changes: batch vs online") 
<br><br>
---

## 2) Problem 4 data

![Problem 1 batch](readme%20images/problem4_batch.PNG "Problem 4 batch: weights changes & Epochs")

- Using this data, the batch calculated the weights very fast since the data was easy to calculate from <br><br><br>

![Problem 1 on-line](readme%20images/problem4_online.PNG "Problem 4 On-line: weights changes & Epochs")

- The batch he was faster than the on-line, which could be from the random weights were initialized better in the batch or since the data is very small it complements the batch algorithm method <br><br><br>

![Problem 4 delta changes](problem4_online_vs_batch.png "Problem 4 delta changes: batch vs online")
<br><br>
---

# <span style="color:#2ac965;"> Generated data from SkLearn</span>

- We will make 2 comparisons here: 
	- The 1st will be with linearly sperable data where the accuracy should be very high in both train and test data
	- The 2nd will be with non-linearly sperable data and see how much error the model will reach

## 1) linearly sperable data

![linearly sperable data batch](readme%20images/linear_batch.PNG "linearly sperable data batch: weights changes & Epochs")

<br><br><br>

![linearly sperable data on-line](readme%20images/linear_online.PNG "linearly sperable data On-line: weights changes & Epochs")

<br><br><br>

![linearly sperable data delta changes](readme%20images/generated_data_online_vs_batch.png "linearly sperable data delta changes: batch vs online")
<br><br>

---

## 1.1) Accuracy Calculations

Here is the data that was generated, which seems very easy for the model to learn from <br>

![linearly sperable data](readme%20images/generated.png "linearly sperable data plot")

<br><br><br>

Now we will plot both models against the test & train data <br>

![linearly sperable models train](readme%20images/training_plot.png "linearly sperable models train plot")

<br><br><br>

![linearly sperable models test](readme%20images/testing_plot.png "linearly sperable models test plot")

<br><br><br>

Finally we calculated for train and test data using both models: confusion matrix, accuracy <br>
The 1st cell is for the batch model, while the second cell is for the on-line model <br>

![linearly sperable train accuracy](readme%20images/linear_train.PNG "linearly sperable models train accuracy")

<br><br><br>

![linearly sperable test accuracy](readme%20images/linear_test.PNG "linearly sperable models test accuracy")

<br>

> Since the data was easy to learn, both models achieved 100% accuracy on both test and train data

<br><br>

---


## 2) non-linearly sperable data

Since the data is not sperable linearly, the model will break at the condition of 10000 & 1000 epochs for batch and on-line respectively

![non-linearly sperable data batch](readme%20images/non_linear_batch.PNG "non-linearly sperable data batch: weights changes & Epochs")

<br><br><br>

![non-linearly sperable data on-line](readme%20images/non_linear_online.PNG "non-linearly sperable data On-line: weights changes & Epochs")

<br><br><br>

![non-linearly sperable data delta changes](readme%20images/generated2_data_online_vs_batch.png "non-linearly sperable data delta changes: batch vs online")
<br><br>

---

## 2.1) Accuracy Calculations

This time we have data which will be very hard to learn on, since it can't be seperated linearly <br>

![non-linearly sperable data](readme%20images/generated2.png "non-linearly sperable data plot")

<br><br><br>

After plotting both models against the test & train data, we can see that the model didn't seperate the data correctly <br>

![non-linearly sperable models train](readme%20images/training2_plot.png "non-linearly sperable models train plot")

<br><br><br>

![non-linearly sperable models test](readme%20images/testing2_plot.png "non-linearly sperable models test plot")

<br><br><br>

Finally we calculated for train and test data using both models: confusion matrix, accuracy <br>
The 1st cell is for the batch model, while the second cell is for the on-line model <br>

![non-linearly sperable train accuracy](readme%20images/non_linear_train.PNG "non-linearly sperable models train accuracy")

<br><br><br>

![non-linearly sperable test accuracy](readme%20images/non_linear_test.PNG "non-linearly sperable models test accuracy")

<br><br><br>

> Since the data was hard to learn, both models achieved lower accuracy on both test and train data than on the linearly sperable data

---
