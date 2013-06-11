![Machine Learning](/2013/06/machine-learning.jpg)

## Prologue
Ever since the dawn of age, man has created tools that facilitate his life and reduce his labour in order to allocate his time and efforts to other tasks that matter more. Over the time, our endeavours exceeded the physical type to include the best of both worlds, the computationally intensive and the physically exhaustive. Consequently our tools had to catch up with our needs and have the capacity to solve those types of problems.

>>// Todo: Talk about a simple instance of the problem and then talk about the large instance. Mention the problem with large numbers of variables (features as refered to in ML) and how we get bored from examining a spreadsheet full of numbers unlike computers, and why we can't examine them in graphic form because of the dimensionality problem. And how reducing the dimensions will obscure and probably hide valuable information for our decision making. Although our brains are good at perception and detecting patterns, the average Joe fails to process massive amounts of data, to come with conclusions. Unlike computers, which can easily consume data, crunch numbers and come up with 

We have the ability to detect patterns, but our brains are not so good with large amounts of numbers.. We could always train ourselves to carry out these tedious tasks, but that won't be much effective; after all it is not every day that we have a new John Nash. There's one way out of this, as the good overlords we've always been, we could delegate these tasks to our faithful minions; by enabling machines to carry out cognitive tasks like pattern recognition and classification.

<!-- TEASER_END -->

## ML Background
Over the last decade, with the increasing interest in the intelligent systems and the rise of big data, machine learning has grown to become ubiquitous in our daily lives.

Some believe that machine learning has emerged from the broad field of Artificial Intelligence, others see both of them as two distinct disciplines that try to solve the problem of intelligence using different approaches; Machine Learning uses statistical, probabilistic and evolutionary approaches, while the Good Old-Fashioned AI relies on symbolic and knowledge based (e.g. expert systems) approaches to attempt to solve this problem.

**Some of the reasons why machine learning emerged:**

- It turns out that it is very hard to write programs that solve some problems like detecting fraud or recognizing objects from different view points, under various conditions i.e. non-uniform illumination. The hardness of this approach is due to the different parameters and really large permutations that one would have to account for in order to solve these problems.
- Even if we figure out some way to write a solution for the problem, there's a great chance that the program will be really complicated.
- There are other problems which involve uncertainty by computing probabilities in order to reach a candidate solution. This means that we need to write programs that combine large numbers of weak rules to reach a final decision.
- Problems themselves might not remain the same and as they evolve with time, consequently we need smart programs that can adapt and detect new patterns as they emerge.

## Definition of Learning
Learning is what gives us the opportunity to adapt and improve our performance in the tasks at hand, learning is what shapes our future experiences. We learn more as we study, practice more and reflect on our experiences; we learn more when we acquire more relevant data. The question now lies in whether we can take this concept and apply it to machines, allow them to learn, to change their state and behaviour as they encounter novel scenarios.

>A computer program is said to learn from experience **E** with respect to some class of task **T** and performance measure **P**, if its performance at tasks in **T**, as measured by **P**, improves with experience **E**.
<cite>Tom Mitchell</cite>

So we can loosely define learning as getting better at a certain task through practising.

// Todo: Talk about an example task 
An example task would be driving cars, the experience would be to drive the car for longer intervals of time and we could measure our performance by minimizing the number of deaths and injuries that magically happen to occur while we are driving.

In the machine learning context, learning is referred to as inductive inference in which we implement algorithms that try to detect patterns presented in a training set or evolving models that occur in the nature and then generalize from them to properly properly solve the problem for new data. The generalisation part is important because no matter how much data we use in the training phase, it is very unlikely that we will see those exact examples again when we put our systems to work.

// Todo: main elements of learning Representation, Evaluation function (objective function), Optimization

The main elements of learning are Representation, Evaluation function (objective function) and Optimization as Pedro Domingos defines them in his article.

## Objective of Machine Learning 

Design efficient, accurate and general learning algorithms that are capable of dealing with large-scale problems in order to make accurate predictions about unseen instances of a given problem.

## Machine Learning in real life

// Todo: Machine learning takes many guises in our everyday life, it has taken .. that we sometimes fail to notice it and take its for granted.

Machine learning is applied in many aspects of our everyday life, even if we fail to take notice of its significance in these fields.

- Handwriting Recognition for tablet devices and smart phones
- Speech Recognition
- Speaker Verification
- Spam Blocking for emails and discussion boards
- Search Engines
- Drug design
- Self-driving(Autonomous) Vehicles. e.g. cars, drones and helicopters
- Monitoring Stock Markets' transactions and detecting malicious behaviours
- Credit Card Fraud Prevention
- Face Recognition e.g. Facebook's Image Tagging
- Recommender Systems e.g. Product and Movie recommendations done by Amazon and Netflix
- Securing Systems against intrusions
- Medical Diagnosis

As you can see, machine learning can be applied to diverse fields causing a really interesting phenomenon to appear, which is the cooperation between different sciences and the combining between them to reach innovative solutions. This multi-disciplinarity as Stephen Marsland refers to, has been embraced yielding many benefits for researchers in the field.

// Todo read this article on collaborative filtering http://www.hindawi.com/journals/aai/2009/421425/
// Todo add the videos https://www.youtube.com/watch?v=JBgG_VSP7f8
## References
- [Stephen Marsland. Machine Learning: An Algorithmic Perspective](http://www.amazon.com/Machine-Learning-Algorithmic-Perspective-Recognition/dp/1420067184)
- [Pedro Domingos. A Few Useful Things to Know about Machine Learning](http://homes.cs.washington.edu/~pedrod/papers/cacm12.pdf)
