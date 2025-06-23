# CODSOFT_CREDITCARDFRAUD
The project is splitted into 2 jupyter notebooks. Documents are named as CreditCardFraud1 and CreditCardFraud2 --> representing analysis and model building(with the preprocessing steps) resp.

About the data = The dataset contains transaction data with features like transaction date and time, credit card number, merchant, category, amount, user details (first name, last name, gender, address, job, date of birth), and location information (latitude, longitude, city population, merchant latitude, merchant longitude). The target variable is_fraud indicates whether a transaction is fraudulent.

SUMMARY FOR CreditCardFraud1: 
Merchant and Category Analysis: 'shopping_net' and 'misc_net' merchant categories show the highest percentage of fraud. Analyzing the top 30 merchants by transaction count also revealed variations in fraud occurrences across different merchants.
Geographic Analysis: Visualizations of fraud distribution by state and city (top 10 by transaction count) indicate that fraud is not uniformly distributed geographically.
Transaction Amount: While most transactions are small, fraudulent transactions appear to have a different distribution of amounts compared to legitimate ones, with some fraudulent transactions having higher values.
Time based Analysis:
Hour of Day: Most fraudulent transactions occur during late night hours, with the lowest frequency during afternoon hours.
Day of Week: There is slight inconsistency in fraudulent transactions across the days of the week.
Month: The analysis by month also shows variations in transaction frequency and fraud distribution.
Demographic Analysis:
Gender: The gender distribution in the dataset is relatively balanced.
Age: Some differences in the number of individuals involved in legitimate or fraudulent transactions were observed across different age ranges.
City Population: There is no clear linear relationship between city population and fraud rate based on the analysis of population bins.
Correlation Analysis: A heatmap of numerical features shows the correlation between different variables. amt and job (after imputation, although the imputation step for 'job' resulted in a TypeError) were noted as potentially more strongly correlated with is_fraud


SUMMARY FOR CreditCardFraud2:
CreditFraud2 was made to run in the T4 GPU runtime mode, so key briefings from this document:-
 PRIMARY STEPS
Loading and inspecting the fraudTrain.csv and fraudTest.csv datasets.
Dropping irrelevant columns like names, street addresses, and transaction numbers.
Handling missing values by dropping rows with NaNs.
Feature engineering by calculating the age of the cardholder from their date of birth and the transaction date.
Extracting time-based features like hour, day of the week, and month from the transaction timestamp.
Dropping the original date/time and date of birth columns.
Encoding categorical features like 'gender', 'category', and 'job' using target-guided ordinal encoding.
Dropping 'merchant', 'city', and 'state' columns based on feature relevance and the creation of a distance feature.
Handling the imbalanced dataset by combining resampling of the majority class with SMOTE for the minority class.
Calculating the Haversine distance between the user's location and the merchant's location as a new feature.
Standardizing the features using StandardScaler.
MODEL BUILDING
Training and evaluating three classification models: Logistic Regression, Decision Tree, and Random Forest.
Performing hyperparameter tuning for Logistic Regression using GridSearchCV.
  KEY FINDINGS
Logistic Regression showed a high overall accuracy but a very low precision for the fraud class (class 1), meaning many transactions predicted as fraud were actually not fraud (high false positives). However, it had a decent recall, indicating it was able to capture a significant portion of the actual fraudulent transactions.
Decision Tree had lower overall accuracy compared to Logistic Regression but a much higher recall for the fraud class. This means it was better at identifying actual fraudulent transactions, but at the cost of a lower precision (more false positives).
Random Forest showed a good balance between precision and recall for the fraud class compared to the other two models. Its accuracy was also high.
