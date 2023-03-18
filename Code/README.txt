############################################################
README file for running code for Assignment 1
############################################################
Student name: Justin Kelley
Student ID: 997351
Subject: COMP30027 (Machine Learning) (Semester 1, 2021)
Assignment: Assignment 1
Date created: 22/03/2021
Date modified: 25/03/2021
############################################################
Overview
############################################################

To find the four main functions preprocess(), train(),
predict() and evaulate(), each are in their own code block
at the end of that code block and seperated from the rest of
the code in that block by seperators like shown below:

#*************************** PRIMARY FUNCTION START *************************#
The function goes here:
#**************************** PRIMARY FUNCTION END **************************#

These functions are coded to perform the basic Gaussian naive bayes
classifer as well as contain code to perform KDE for questions 3
and 4. These functions do this with the help of some helper functions
and what they do depends on the arguements given. The runModel()
function determines what these functions will do. For example, they can be
run to perform Gaussian Naive Bayes or KDE Naive Bayes. How to use this
function is explained below.

############################################################
How to run Code
############################################################

The code for the basic classifier and for questions 3 and 4
are combined together, but can be run seperately by using the
runModel() driver function, which is located in the last
code block before the questions at the bottom with seperators:

#**************************** DRIVER FUNCTION END ***************************#
def runModel():
    code goes here:
#**************************** DRIVER FUNCTION END ***************************#

The call to this function to run it is just below this. In order to run this function,
the code blocks above it must be run first in order to initialise the function definations,
imports and constants.

This function has calls to several functions that will run other functions located
above it in the same block code. These functions will run preprocess(), train(),
predict(), evaulate() and other functions to perform Gaussian Naive Bayes, KDE
Naive Bayes with arbitrary kernel bandwidth or KDE Naive Bayes with kernel
bandwidth choosen by cross-validation. These functions run these classifiers under
different circumstances such as changing the files used for training and testing.

Comment or uncomment these functions to run them. One, more or all of them can be
run at the same time.

For example, the runBasic() function will run the classifier for Gaussian
naive bayes using train.csv and test.csv for training and testing. This is
the most basic functionaility required before answering any questions. The
remaining functions below this one are for questions 3 and questions 4. This
function produces the output shown in Figure 1.

The runDefault() function is next and is used to produce Figure 2. It runs
both the KDE with kernel bandwidth (KB) equal to 5 and Gaussian naive bayes
methods using train.csv and test.csv for training and testing. This is used
to compare results of these two approaches for question 3.

The runDefaultWithCrossValidation() function is used to produce Figure 3. It runs
both the KDE with kernel bandwidth (KB) using randomised cross validation
and Gaussian naive bayes methods using train.csv and test.csv for training and testing.
This is used to compare results of these two approaches for question 4.

The runDefaultWithWholeDataSet() function is next and is used to produce Figure 4. It runs
both the KDE with kernel bandwidth (KB) equal to 5 and Gaussian naive bayes
methods using train.csv and combined.csv for training and testing. This is used
to compare results of these two approaches for question 3 when we try to over fit
the model using the training set as part of the testing set.

The runUsingWholeDataSet() function is used to produce Figure 5. It runs
both the KDE with kernel bandwidth (KB) using randomised cross validation
and Gaussian naive bayes methods using train.csv and combined.csv for training
and testing. This is used to compare results of these two approaches for question 4
when we try to over fit the model using the training set as part of the testing set.

The runKDEWithDifferentKBs() function is used to produce Figure 6. It runs
the KDE classifier with a range of different KBs using train.csv and test.csv for training
and testing. This is used to see the effect of different KBs on accuracy score for
the KDE classifier for question 3.

The runKDEWithCrossValidationWithInfo() function is used to produce Figure 7. It runs
the KDE classifier with a range of different numbers of partitions (m) using
randomised cross-validation. The train.csv and test.csv files are used for training
and testing. This is used to see the effect of different values for m on accuracy score for
the KDE classifier for question 4 and provide additional information of the underlying
algorithm.

The runKDECrossValidationWithNoShuffling() function is used produce Figure 8. It runs
the KDE classifier with a range of different numbers of partitions (m) using
cross-validation. The train.csv and test.csv files are used for training
and testing. This is used to see the effect of not shuffling the instances
before doing cross-validation on the performance of selecting a value for KB.
Compare these results to Figure 7 where the scores for different KBs for a choosen m
vary more. In Figure 8 all KBs give the same score for some values of m.

############################################################
Example 1 (Gaussian Naive Bayes)
############################################################

To run the basic Gaussian Naive Bayes classifier only, comment
all function calls in runModel(), except for runBasic() as shown below:

#**************************** DRIVER FUNCTION END ***************************#
def runModel():
    """This functions runs the naive bayes model under different circumstances."""
    # Each of these functions will run the naive bayes classifer under different
    # situations. Comment or uncomment the function to run it. Use the README file
    # for further details.
    
    # Run the Gaussian using the normal train and testing data sets.
    runBasic()
    
    # Run the Gaussian and KDE (with kernal bandwidth of 5) naive bayes models
    # using the normal train and testing data sets.
    #runDefault()
    
    # Run the Gaussian and KDE (with kernal bandwidth selected via cross validation)
    # naive bayes models using the normal train and testing data sets.
    #runDefaultWithCrossValidation()
    
    # Run the Gaussian and KDE (with kernal bandwidth of 5) naive bayes models
    # using the whole data set as testing.
    #runUsingWholeDataSet()
    
    # Run the Gaussian and KDE (with kernal bandwidth selected via cross validation)
    # naive bayes models using the whole data set as testing."""
    #runUsingWholeDataSetWithCrossValidation()
    
    #Run the Gaussian naive bayes model using a range of KBs
    # using both training and testing data sets.
    #runKDEWithDifferentKBs()
    
    # Run the Gaussian naive bayes model using a range of Ms
    # using both training and testing data sets.
    #runKDEWithCrossValidationWithInfo()
    
    # Run the Gaussian naive bayes model using a range of Ms
    # using both training and testing data sets without random
    # shuffling to demonstrate the consquences.
    # runKDECrossValidationWithNoShuffling()
    
    return 0
#**************************** DRIVER FUNCTION END ***************************#

This will run the following function:

def runBasic():
    """Runs the Gaussian naive bayes models
    using the normal train and testing data sets."""
    
    # Get training and testing data sets from files.
    xTrain, yTrain, xTest, yTest = preprocess("train.csv", "test.csv")
    
    # Compute priors and likelihoods.
    priors, likelihoods = train(xTrain, yTrain)
    
    # Run naive bayes using Gaussian method.
    predictionsGaussian = predict(xTest, yTest, priors, likelihoods, "Gaussian")
    
    # Compute accuracy score.
    scoreGaussian = evaluate(predictionsGaussian, yTest)

    # Display results.
    print(PRIMARY_DIVIDER)  
    print(f"Gaussian naive bayes with default data set has accuracy score {round(scoreGaussian, 3)}.")
    print(PRIMARY_DIVIDER) 
    print()
    print()
    
    return 0

That will perform Guassian Naive Bayes and produce output:

######################################################################
Gaussian naive bayes with default data set has accuracy score 0.716.
######################################################################







############################################################
Example 2 (Comparing Gaussian and KDE Naive Bayes)
############################################################

To compare the results of Gaussian and KDE Naive Bayes comment
all function calls in runModel(), except for runDefault() as shown below:

#**************************** DRIVER FUNCTION END ***************************#
def runModel():
    """This functions runs the naive bayes model under different circumstances."""
    # Each of these functions will run the naive bayes classifer under different
    # situations. Comment or uncomment the function to run it. Use the README file
    # for further details.
    
    # Run the Gaussian using the normal train and testing data sets.
    #runBasic()
    
    # Run the Gaussian and KDE (with kernal bandwidth of 5) naive bayes models
    # using the normal train and testing data sets.
    runDefault()
    
    # Run the Gaussian and KDE (with kernal bandwidth selected via cross validation)
    # naive bayes models using the normal train and testing data sets.
    #runDefaultWithCrossValidation()
    
    # Run the Gaussian and KDE (with kernal bandwidth of 5) naive bayes models
    # using the whole data set as testing.
    #runUsingWholeDataSet()
    
    # Run the Gaussian and KDE (with kernal bandwidth selected via cross validation)
    # naive bayes models using the whole data set as testing."""
    #runUsingWholeDataSetWithCrossValidation()
    
    #Run the Gaussian naive bayes model using a range of KBs
    # using both training and testing data sets.
    #runKDEWithDifferentKBs()
    
    # Run the Gaussian naive bayes model using a range of Ms
    # using both training and testing data sets.
    #runKDEWithCrossValidationWithInfo()
    
    # Run the Gaussian naive bayes model using a range of Ms
    # using both training and testing data sets without random
    # shuffling to demonstrate the consquences.
    # runKDECrossValidationWithNoShuffling()
    
    return 0
#**************************** DRIVER FUNCTION END ***************************#

This will run the following function:

def runDefault():
    """Runs the Gaussian and KDE (with kernal bandwidth of 5) naive bayes models
    using the normal train and testing data sets."""
    
    # Get training and testing data sets from files.
    xTrain, yTrain, xTest, yTest = preprocess("train.csv", "test.csv")
    
    # Compute priors and likelihoods.
    priors, likelihoods = train(xTrain, yTrain)
    
    # Run naive bayes using Gaussian and KDE with kernel bandwidth of 5.
    predictionsGaussian = predict(xTest, yTest, priors, likelihoods, "Gaussian")
    predictionskDE = predict(xTest, yTest, priors, groupByClass(xTrain, yTrain), "KDE")
    
    # Compute accuracy scores for each method.
    scoreGaussian = evaluate(predictionsGaussian, yTest)
    scoreKDE = evaluate(predictionskDE, yTest)

    # Display results.
    print(PRIMARY_DIVIDER)  
    print(f"Gaussian naive bayes with default data set has accuracy score {round(scoreGaussian, 3)}.")
    print(DIVIDER)
    print(f"KDE naive bayes with default data set and kernel bandwidth of 5 has accuracy score {round(scoreKDE, 3)}.")
    print(PRIMARY_DIVIDER)
    print()
    print()
    
    return 0

Which will product output:

######################################################################
Gaussian naive bayes with default data set has accuracy score 0.716.
*******************************************************************
KDE naive bayes with default data set and kernel bandwidth of 5 has accuracy score 0.767.
######################################################################

############################################################



















