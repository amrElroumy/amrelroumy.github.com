# Learnig Methods

The main learning methods applied in machine learning which differ based on the problem at hand are divided into four types:

- Supervised Learning
- Unsupervised Learning
- Reinforcement Learning
- Evolutionary Learning

The distinction between those learning methods lies in the way the algorithm evaluates its actions and 

## Supervised Learning
Supervised Learning–sometimes referred to as learning with a teacher–which is one of the important tasks in machine learning, is carried out by presenting to the algorithm a dataset with all the right answers (desired outcome) labelled. This obviously is helpful as it enables us to show the algorithm the right answer to the sample data and allow it to learn from them, in order to predict right answers for new instances of the problem.  

Supervised Learning's method of work mainly depends on an algorithm that tries to understand the relationship between a dependent variable and the independent variables (features) characterizing an instance of the problem, and based on this relationship produces a mapping between the input data and a classification/prediction.

Problems that can be solved by supervised learning can either be classification problems, or regression problems. The distinction mainly lies whether the answer is discrete or real-valued (continuous).

### Classification Problem
A problem in which we want to predict a discrete valued output. Examples for this type of problems include:

- predicting the probability(chance) that a patient has cancer or not
- a person in a picture is either male or female
- a mail that you received is spam or not
- the blood type of a patient ("A", "B", "AB" or "O").  

### Regression Problem
A problem in which we want to predict a continuous valued output, which could be either a real number or a whole vector of real numbers.

Examples of problems that are classified as regression problems:
- The price of a stock in 6 months time.
- The temperature at noon next weekend.

## Unsupervised learning
The problems that unsupervised learning tries to solve, is to find internal representation (structure) between the input data; that is it tries to figure out if there are points of similarity/dissimilarity between the input and sort them out according to them.

For almost 40 years, the machine learning community ignored unsupervised learning except for one form which is clustering. One reason for this was that it was hard to say exactly the aim of unsupervised learning. One major aim is to create an internal representation of the input that could be useful for subsequent supervised or reinforcement learning.

Another important aim would be to construct a low-dimensional representation of the input.
Example: Handwriting recognition, in which having images with millions of pixels doesn't necessarily mean that we have million degrees of freedom to construct digits and letters. Instead, we could find a way to represent the possible hundreds of degrees of freedom which would suffice to recognise the different handwritings.

### Clustering
Finding structure in unlabelled data upon which we can break data into separate clusters.

## Reinforcement learning
Reinforcement learning, is like training a pet 
// Todo: Continue the example

So to put it formally, in reinforcement learning the output is an action or a sequence of actions that are carried out by an agent, and the only supervisory signal the algorithm receives is an occasional scalar reward which could be affected by a discount factor if it is somehow delayed. This prevents the algorithm from looking too far into the future.

The difficulty of reinforcement learning lies in the fact that rewards are typically delayed, making it hard to know where the algorithm went wrong or right. In addition, scalar rewards don't provide much feedback on which we could base the changes in the parameters making it less feasible to learn millions of parameters using reinforcement learning which, on the contrary, is feasible using both supervised and unsupervised learning.


// Todo: Needs improvement
For example: If we want to train an algorithm to have a sophisticated vision system like ours, the most intuitive thing to do (if we want it to learn by itself) would to have it use the disparity of the perceived stereo images in order to deduce the distance between it and the observed object. Certainly we don't want to use the pay-offs of reinforcement learning to set our parameters, as this would be like repeatedly stubbing our toes and adjusting our parameters based on our observations in order to calibrate the distance.

## Evolutionary learning
