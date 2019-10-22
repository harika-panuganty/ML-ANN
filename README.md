# ML-ANN

This is the ANN week project for my Intermediate Applied Data Analysis class from the MscBMI Program at The University of Chicago tested on Linear Regression in R. The code for this repository elaborates on the specific code used to  running Artificial Neural Network (ANN) Models for three Kaggle datasets in R:

1. A large patient readmission dataset https://inclass.kaggle.com/c/predicting-30-day-hospital-readmissions

2. A medium sized patient laboratory values dataset https://www.kaggle.com/c/gusto/data

3. A primate junction splice sequence dataset https://inclass.kaggle.com/c/cs529-project1/data (significant challenges due to nucleotide format of data). This dataset included three outcome variables (IE, EI and N) therefore there are models for each variation of a combination of the three variables.

ANN Model: I first centered and scaled the train data (using R function preProcess) to prepare to run a neural network, creating the new test and train datasets for the model. After changing the outcome of variable to factors and assigning them 'levels' of 0 and 1, the next step is to create an ObjGrid that takes into account the following parameters: the size of the neural network (this model began at layer 2 and ended at layer 30, separated by 1) and the decay rate (was 1e-04 for this model). These parameters were input into the expand.grid function and FitControl took into account the method “cv” and the number 5 which indicates a 5-fold cross validation. In this training model, the data used is the new gusto train data, method is ‘nnet, tuneGrid is the objGrid,  trControl is fitControl and trace is FALSE. Using the trained data, test data was predicted using R function predict() with object being gusto trained model, dataset is the gusto test, and type being ‘prob’. The predicted nnet outcome was derived from the predicted data and `1` (the outcome we are looking for). The ‘perf’ model was a roc function that took into account a response and a predictor. AUC and 95% CI was printed to check accuracy of the model.

Note: For the readmissions dataset, SMOTE was used as the data was imbalanced. The original dataset had an un-even distribution of 0s and 1s, making the model difficult to predict when faced with the test dataset. The SMOTE dataset resulted in a smaller train dataset and had a more equal distribution of the two outcomes.
