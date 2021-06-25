Here we have to identify the gene variation, and have to identify between 9 types of cancer(1-9).

We have to automate the manual process of the domain experts to classify the cancer.
Data from Kaggle.com
we have training_text and training_variants.
Training_text is made using a research on the 1000s of gene variations and provided for easiness.

Understanding data

In Data_variants: ID, Gene, Variants, and Class(this is the various cancers from 1 to 9).

So We have Gene, Variation, Text(from Research Paper) from 2nd dataset we will predict the class. 
In The Data_text we have the text needed for the particular variation.

This is a Multi Class Clasification Problem.

This is a Medical Problem. So errors should be reduced. Accuracy is very important.
Probability of each class is needed.
Reasoning the results given by the Model is Good. So Interpretatibility of the model should be good.
RBF, SVM are not so interpretable.
Naive Bayes, Decision Tree, Logistic Regression, Linear SVM are interpretable.

Latency: Can give flexibility on it.

Data Processing:

removing Stop Words, special Characters, etc.
merging both the data to one.
Dealing with missing Data. imputation on null texts simpily by merging Gene and Variation column.

Creating Training, Test and Validation data
100 -> 80, 20
80  -> 80, 20

Now we have to check whether the data distribution has happened properly.
So we have to do a value_counts.
Make it into a graph

Our Evaluation Criteria:    Multi Class Log Loss

-1/n(sum along all rows(sum along all classes((yc)log(pc))))
where yc = 0 or 1
and pc =probability to be in class c 

for comparision w.r.t MultiClass LogLoss we will create a Random Model.
just simply do the prediction and confusion matrix and all(precision recall etc).

Now we will analyse the impactness of all the columns(Gene) to the class.
So Gene it is catagorical.
By the Analysis on Gene, around 50 genes out of 232 are contributing to the 75% of the data.

Now we have to convert the Gene data so as it's feedable to the model we are making.
    1. One-hot Encoding.(creates a lot of columns, which are parse, increases dimensionality of data)
    Logistic Regression, linear-SVM workes well
    2. Response Encoding(or Mean impuation, in this we will replace that categorical value into something meaningful. eg: Average height of the people in a region etc...(it's an art)).
    Naive Bayers, Random Forest,KNN works well
        here,
        we  have gene and class, so in Response Encoding, for every row, we will create 9 columns with the value Probability of y = i, given the gene Gi. where i is from 1 to 9.
        (Bayer's Theorem, conditional probability)
        So now we only have 9 columns.
        Along with this we will do the Laplace encoding.
Now we can make a model with Gene column(I mean the transformed one) to predict the Class and compare it with the Random model(log loss). Then we will get an idea of the importance of Gene column.
 

Callibirated Classifier: Mainly used to get the output as probability as sometimes our model won't give ouput in probability so to calculate the log-loss we can use it. 

xi ---> M ---> yi -----> Classifier(sigmoid or isotonic function) ---> y(probability)

SGD(siostatic Gradient Desient): it's for optimization purpose.

Also we have to check how stable is the model. i.e we should have a good overlap with the data in the train and cv else no use of training.

For Variation column :
it's not stable, and but log loss is okay
so We even can remove it.

Similarly do for text column
 There also we can do one-hot Encoding and also Response Encoding(a new 9 more columns).

after this make a model with text column.

From all these all the columns are important.

Now We combine all the colums which are processed.

Building ML model

    Naive Bayers
    KNN
    Logistic Regression(With Balancing): Balancing(OverSampling) has some effects on the output
    Logistic Regression without Balancing
    Linear SVM
    RFC
Stacking method woks very well with huge amount of data else it won't work good.




We very Quickly went to bag of words and used CountVectorizor.
We can use TFIDF. 

