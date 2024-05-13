# Deep Learning Challenge Report

## Purpose of Analysis
The nonprofit foundation Alphabet Soup wants a tool that can help it select the applicants for funding with the best chance of success in their ventures. With your knowledge of machine learning and neural networks, you’ll use the features in the provided dataset to create a binary classifier that can predict whether applicants will be successful if funded by Alphabet Soup.

## Data Preprocessing
The first step I took was to load in all of my required dependencies including sklearn's train_test_split and StandardScaler, pandas, and tensorflow.
I read in the charity_data.csv file as a pandas dataframe under the variable name "application_df".
Knowing that I was building a predictive model that would attempt to predict which previous applicants had used funds successfully, there would be some columns that would be useless for the predictive model we were trying to build. In this case those columns are 'EIN' and 'NAME' neither of which have any real affect on our eventual y, which is the 'IS_SUCCESSFUL' column.
The rest of our columns are features of our predictive model, but there needed to be some work done to limit the affect rare values within the columns would have, so I looked at the value counts for the 'APPLICATION_TYPE' and 'CLASSIFICATION' and classified 'APPLICATION_TYPE value counts below 500 as rare and reidentified them as 'other'. Value counts below 1000 were identified as rare for 'CLASSIFICATION'. After looking at the data, the cut-offs were chose because the vast majority of the value_counts existed above those two cut lines.

Once I had sucessfully done that, I began the process of setting up the model by creating dummies of the application_df, setting up x as all columns that aren't 'IS_SUCCESSFUL' and y as the 'IS_SUCCESSFUL' column. Once that was completed, I set up the training and testing datasets using train_test_split, and ran the x_train and x_test variables through the StandardScaler.

## Building the Models
For my original model, I chose two hiden layers with node values of 15 and 10 respectively. I used the acctivation of "relu" for both the hidden layers and the output layer. I realize now that the number of nodes was likely overfitting my data due to the low accuracy at the end of the model. After I compiled the model, I trained it using 11 epochs because when I searched how many I should use (I wasn't sure) datascientest.com recommended using 11. (Source:https://datascientest.com/en/epoch-an-essential-notion#:~:text=A%20larger%20number%20of%20epochs,to%20optimally%20modify%20the%20weights.) Unfortunately, this model only gave me an accuracy level of 57.05%.

On my second model, I decided to add a third neural layer with 5 nodes to try to boost the accuracy. I also upped the number of epochs to 20 after running it at 11 and seeing that the accuracy didn't increase. Even after making that adjustment, I only achieved an accuracy of 57.47%, which is an incredibly slight improvement.

At this point I realized I needed to rethink my approach. I decided to make two changes. The first was that I decided to lower the number of nodes in each of the hidden layers. I used 10, 8, and 5 respectively. The second was that I decided to switch from rectified linear ('relu') as my activation, and go with an activator that is less linear like 'sigmoid'. I ran this with 20 epochs again, and achieved 70.17% accuracy, which was a much better improvement over model 2, but still not reaching our goal of 73%. According to the assignment, I could have stopped here, but I don't like admitting defeat.

On my fourth and (thankfully) final model, I decided to use a combination of relu on the first hidden layer and sigmoid on the rest of the layers. I also upped the number of epochs to 30 to see if I could improve just a few percentage points to hit the 73%. On this final model, I achieved 79% accuracy.

Once completed, I exported my model as an HDF5 file.
