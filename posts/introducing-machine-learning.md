## Introduction
Some believe that machine learning has emerged from the broad field of Artificial Intelligence, others see both of them as two distinct disciplines that try to solve the problem of intelligence using different approaches; Machine Learning uses statistical, probabilistic and evolutionary approaches, while the Good Old-Fashioned AI relies on symbolic and knowledge based (i.e. expert systems) approaches to attempt to solve this problem.

In the ML context, learning is referred to as inductive inference in which we implement algorithms that try to detect patterns presented in small datasets and to generalize from them to form statistical models which allow them to evolve and adapt.

## Definition
>A computer program is said to learn from experience **E** with respect to some class of task **T** and performance measure **P**, if its performance at tasks in **T**, as measured by **P**, improves with experience **E**.
<cite>Tom Mitchell</cite>


**Some of the reasons why machine learning emerged:**

- It turns out that it is very hard to write programs that solve some problems like detecting fraud (detect malicious patterns) or recognizing objects from different view points and under various conditions i.e. non-uniform illumination. The hardness of this approach results from the different parameters and really large permutations that one would have to account for in order to solve these problems.
- Even if we figure out some way to write a solution for the problem, there's a great chance that the program will be really complicated.
- There are other problems which involve uncertainty by computing probabilities in order to reach a candidate solution. This means that we need to write programs that combine large numbers of weak rules to reach a final decision.
- Problems themselves might not remain the same and as they evolve with time, consequently we need smart programs that can adapt and detect new patterns as they emerge.

## Objective of Machine Learning 

Design efficient, accurate and general learning algorithms that are capable of dealing with large-scale problems in order to make accurate predictions about unseen instances of a given problem.

## Machine Learning in real life

Machine learning is applied in many aspects of our everyday life, even if we fail to take notice of its significance in these fields.

- Handwriting Recognition for tablet devices and smart phones
- Speech Recognition e.g. Google Search and Siri
- Speaker Verification for security systems
- Spam Blocking in our emails
- Search Engines
- Self-driving(Autonomous) Vehicles. e.g. cars, drones and helicopters
- Monitoring Stock Markets' transactions and detecting malicious behaviours
- Credit Card Fraud Prevention
- Face Recognition e.g. Facebook's Image Tagging
- Recommender Systems e.g. Product recommendation done by Amazon and Netflix
- Securing Systems against intrusions
- Medical Diagnosis

## Major Classes of Learning Algorithms

- Supervised Learning
- Unsupervised Learning
- Reinforcement Learning

## Supervised Learning
Supervised Learning–sometimes referred to as learning with a teacher–is carried out by presenting to the algorithm a dataset with all the right answers labelled, and then the algorithm tries to predict other right answers.  

Supervised Learning method of work mainly depends on an algorithm that tries to understand the relationship between a dependent variable and the independent variables (features) extracted from a given dataset, and based on this relationship attempts produce valid results for other instances of the problem.  

Problems that can be solved by supervised learning can either be classification problems, or regression problems. The distinction mainly lies whether the answer is discrete or real-valued (continuous).

### Classification Problem
A problem in which we want to predict a discrete valued output. Example for this type of problems is predicting the probability(chance) that a patient has cancer or not, a person in a picture is either male or female, a mail that you received is spam or not, or the blood type of a patient ("A", "B", "AB" or "O").  


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
Finding structure in unlabelled data and break data into separate clusters.

## Reinforcement learning
In reinforcement learning the output is an action or a sequence of actions that when carried out, and the only supervisory signal the algorithm receives is an occasional scalar reward which could be affected by a discount factor if it is somehow delayed. This prevents the algorithm from looking too far into the future.

The difficulty of reinforcement learning lies in the fact that rewards are typically delayed, making it hard to know where the algorithm went wrong or right. In addition, scalar rewards don't provide much feedback on which we could base the changes in the parameters making it less feasible to learn millions of parameters using reinforcement learning which, on the contrary, is feasible using both supervised and unsupervised learning.

For example: If we want to train an algorithm to have a sophisticated vision system like ours, the most intuitive thing to do (if we want it to learn by itself) would to have it use the disparity of the perceived stereo images in order to deduce the distance between it and the observed object. Certainly we don't want to use the pay-offs of reinforcement learning to set our parameters, as this would be like repeatedly stubbing our toes and adjusting our parameters based on our observations in order to calibrate the distance.

---

## Regression Problem
Methods to solve include:

- Gradient Descent

## Classification Problem
Methods to solve include:

- Logistic Regression 

### Logistic Regression
Is characterized by producing a hypothesis (h&theta;(x)) which is bounded by 0, 1, so it can be used with classification problems of two classes **0 <= h&theta;(x) <= 1)**  
It is only named regression for historical reasons, but it is a classification algorithm.

