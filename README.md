## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.

STEP 2:Clean the Data Set using Data Cleaning Process.

STEP 3:Apply Feature Encoding for the feature in the data set.

STEP 4:Apply Feature Transformation for the feature in the data set.

STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.

2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.

3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.

4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation

• Reciprocal Transformation

• Square Root Transformation

• Square Transformation

  # 2. POWER TRANSFORMATION
• Boxcox method

• Yeojohnson method

# CODING AND OUTPUT:

1. Data_to_transform.csv dataset
~~~
# Step 1: Import Necessary Libraries
import pandas as pd
import numpy as np
from sklearn.preprocessing import LabelEncoder, StandardScaler, PowerTransformer
from scipy.stats import boxcox
# Step 2: Load the Dataset
data = pd.read_csv('Data_to_Transform.csv')
print("Original Dataset:")
print(data.head())
~~~

<img width="830" height="350" alt="Screenshot 2026-03-09 211430" src="https://github.com/user-attachments/assets/c7cfe8e4-ec32-48bb-8f25-1bcca54a1c2d" />

~~~
# Step 3: Handle Missing Values (Fill numeric columns with mean)
data.fillna(data.mean(numeric_only=True), inplace=True)

# Select a suitable numeric column for transformation
numeric_column = data.select_dtypes(include=np.number).columns[0]

print(f"\nColumn Selected for Transformation: {numeric_column}")

# Keep only positive values for log and boxcox
positive_data = data[data[numeric_column] > 0].copy()
~~~

<img width="661" height="88" alt="Screenshot 2026-03-09 211603" src="https://github.com/user-attachments/assets/4d1ccc8d-b440-48df-b4ab-70f554064bbf" />

~~~
# Step 4: Log Transformation
positive_data['Log_Transform'] = np.log(positive_data[numeric_column])
# Step 5: Reciprocal Transformation
positive_data['Reciprocal_Transform'] = 1 / positive_data[numeric_column]
# Step 6: Square Root Transformation
positive_data['Sqrt_Transform'] = np.sqrt(positive_data[numeric_column])
# Step 7: Square Transformation
positive_data['Square_Transform'] = np.square(positive_data[numeric_column])
# Step 8: Box-Cox Transformation (only positive values)
positive_data['BoxCox_Transform'], lambda_value = boxcox(positive_data[numeric_column])

print(f"\nBox-Cox Lambda Value: {lambda_value}")
~~~

<img width="474" height="59" alt="Screenshot 2026-03-09 211743" src="https://github.com/user-attachments/assets/7b9022b5-d874-42df-b8f2-f3279090dda4" />

~~~
# Step 9: Yeo-Johnson Transformation (works with zero/negative values)
pt = PowerTransformer(method='yeo-johnson')
data['YeoJohnson_Transform'] = pt.fit_transform(data[[numeric_column]])

# Standard Scaling
scaler = StandardScaler()
data['Standard_Scaled'] = scaler.fit_transform(data[[numeric_column]])

# Save the transformed dataset
positive_data.to_csv('Transformed_Positive_Data.csv', index=False)
data.to_csv('Transformed_Full_Data.csv', index=False)

print("\nTransformation Completed Successfully.")
print("\nTransformed Dataset Preview:")
print(positive_data.head())
~~~

<img width="810" height="610" alt="Screenshot 2026-03-09 211826" src="https://github.com/user-attachments/assets/9acb6b33-d888-4768-b504-b3c0e222ce4a" />


2. data.csv dataset

~~~
# Step 1: Import Necessary Libraries
import pandas as pd
import numpy as np
from sklearn.preprocessing import LabelEncoder, StandardScaler, PowerTransformer
from scipy.stats import boxcox
# Step 2: Load the Dataset
data = pd.read_csv('data.csv')

print("Original Dataset:")
print(data.head())
~~~

<img width="658" height="211" alt="Screenshot 2026-03-09 211921" src="https://github.com/user-attachments/assets/f706de1c-948c-4f93-86ce-a28ddb48070e" />

~~~
# Step 3: Handle Missing Values (Fill numeric columns with mean)
data.fillna(data.mean(numeric_only=True), inplace=True)

# Select a suitable numeric column for transformation
numeric_column = data.select_dtypes(include=np.number).columns[0]

print(f"\nColumn Selected for Transformation: {numeric_column}")

# Keep only positive values for log and boxcox
positive_data = data[data[numeric_column] > 0].copy()
~~~

<img width="457" height="69" alt="Screenshot 2026-03-09 211959" src="https://github.com/user-attachments/assets/ddedd561-edac-4a06-822f-3319cd91178c" />

~~~
# Step 4: Log Transformation
positive_data['Log_Transform'] = np.log(positive_data[numeric_column])
# Step 5: Reciprocal Transformation
positive_data['Reciprocal_Transform'] = 1 / positive_data[numeric_column]
# Step 6: Square Root Transformation
positive_data['Sqrt_Transform'] = np.sqrt(positive_data[numeric_column])
# Step 7: Square Transformation
positive_data['Square_Transform'] = np.square(positive_data[numeric_column])

# Step 8: Box-Cox Transformation (only positive values)
positive_data['BoxCox_Transform'], lambda_value = boxcox(positive_data[numeric_column])

print(f"\nBox-Cox Lambda Value: {lambda_value}")
~~~

<img width="467" height="61" alt="Screenshot 2026-03-09 212108" src="https://github.com/user-attachments/assets/ce139e63-de3a-40a0-b299-979473ad2015" />

~~~
# Step 9: Yeo-Johnson Transformation (works with zero/negative values)
pt = PowerTransformer(method='yeo-johnson')
data['YeoJohnson_Transform'] = pt.fit_transform(data[[numeric_column]])

# Standard Scaling
scaler = StandardScaler()
data['Standard_Scaled'] = scaler.fit_transform(data[[numeric_column]])

# Save the transformed dataset
positive_data.to_csv('Transformed_Positive_Data.csv', index=False)
data.to_csv('Transformed_Full_Data.csv', index=False)

print("\nTransformation Completed Successfully.")
print("\nTransformed Dataset Preview:")
print(positive_data.head())
~~~

<img width="817" height="449" alt="Screenshot 2026-03-09 212148" src="https://github.com/user-attachments/assets/0c5eb25d-b148-4186-aad0-86e56df0d780" />

3. Encoding Data.csv dataset

~~~
# Step 1: Import Necessary Libraries
import pandas as pd
import numpy as np
from sklearn.preprocessing import LabelEncoder, StandardScaler, PowerTransformer
from scipy.stats import boxcox
# Step 2: Load the Dataset
data = pd.read_csv('Encoding Data.csv')

print("Original Dataset:")
print(data.head())
~~~

<img width="389" height="215" alt="Screenshot 2026-03-09 212248" src="https://github.com/user-attachments/assets/3b5e1da7-be65-4c09-a06e-3df9b9805705" />

~~~
# Step 3: Handle Missing Values (Fill numeric columns with mean)
data.fillna(data.mean(numeric_only=True), inplace=True)

# Select a suitable numeric column for transformation
numeric_column = data.select_dtypes(include=np.number).columns[0]

print(f"\nColumn Selected for Transformation: {numeric_column}")

# Keep only positive values for log and boxcox
positive_data = data[data[numeric_column] > 0].copy()
~~~

<img width="478" height="45" alt="Screenshot 2026-03-09 212333" src="https://github.com/user-attachments/assets/bcf6293d-4cd8-4147-9318-604899b68ac9" />

~~~
# Step 4: Log Transformation
positive_data['Log_Transform'] = np.log(positive_data[numeric_column])
# Step 5: Reciprocal Transformation
positive_data['Reciprocal_Transform'] = 1 / positive_data[numeric_column]
# Step 6: Square Root Transformation
positive_data['Sqrt_Transform'] = np.sqrt(positive_data[numeric_column])
# Step 7: Square Transformation
positive_data['Square_Transform'] = np.square(positive_data[numeric_column])
# Step 8: Box-Cox Transformation (only positive values)
positive_data['BoxCox_Transform'], lambda_value = boxcox(positive_data[numeric_column])
print(f"\nBox-Cox Lambda Value: {lambda_value}")
~~~

<img width="468" height="81" alt="Screenshot 2026-03-09 212434" src="https://github.com/user-attachments/assets/5ce309e5-303f-4cf5-b836-696e83295806" />

~~~
# Step 9: Yeo-Johnson Transformation (works with zero/negative values)
pt = PowerTransformer(method='yeo-johnson')
data['YeoJohnson_Transform'] = pt.fit_transform(data[[numeric_column]])

# Standard Scaling
scaler = StandardScaler()
data['Standard_Scaled'] = scaler.fit_transform(data[[numeric_column]])

# Save the transformed dataset
positive_data.to_csv('Transformed_Positive_Data.csv', index=False)
data.to_csv('Transformed_Full_Data.csv', index=False)

print("\nTransformation Completed Successfully.")
print("\nTransformed Dataset Preview:")
print(positive_data.head())
~~~

<img width="713" height="446" alt="Screenshot 2026-03-09 212518" src="https://github.com/user-attachments/assets/45df5a0f-a3ec-46ad-a4d3-37cf91d2edcb" />



# RESULT:
    Thus for the given dataset we performed Feature Encoding and Feature Transformation processes, and saved the transformed data to a file.
      

       
