# Lab-Based-ICU-Stay-Length-Prediction-for-Cardiac-Surgery-Patients
Neither code nor data are provided due to confidentiality reasons

## Project Intuition
Integrating some of the diverse data collected from patients during their hospital stay to roughly estimate the length of their stay in the intensive care unit for logistic reasons; primarily to plan patient flow through the unit as to efficiently accommodate as many patients as possible, with AICU having 20  beds and PICU having 12, in unit time with the effectivequality of healthcare already delivered.

![image](https://user-images.githubusercontent.com/81769303/205239089-09046369-e1ea-4590-9d57-c078d040e75e.png)

## Project Pipeline

![image](https://user-images.githubusercontent.com/81769303/205239345-edc40cf9-acc2-4241-9e95-f0dc015660cb.png)

## Project Data

![image](https://user-images.githubusercontent.com/81769303/205239511-cfc25c71-80a6-4dc4-a665-ddc5318741cd.png)

## Data Validation
Data quality assessment is performed where missing, duplicated and outdated data are handled, and invalid or cases irrelevant to project scope are reported.
### Samples
- If a patient visit consists only of an Admission event followed by a Cancel Admission event

![image](https://user-images.githubusercontent.com/81769303/205240130-590ba8ee-67cc-470c-94d5-702da403912b.png)

Sample Visit:

![image](https://user-images.githubusercontent.com/81769303/205240203-c68297e9-01fa-4f95-8fe5-c6b1d68ac255.png)

- If a patient visit includes neither OR nor ICU as visited units

![image](https://user-images.githubusercontent.com/81769303/205240325-722a8886-eec4-4c99-8080-d2765c50ddb0.png)

Sample Visit:

![image](https://user-images.githubusercontent.com/81769303/205240386-b008bb68-e0eb-4c54-b0c0-765eded61d48.png)

- If a patient visit has a missing Transfer From/Transfer To event

![image](https://user-images.githubusercontent.com/81769303/205240481-3b254a3e-867b-40d9-9e12-079ee3846e00.png)

Sample Visit:

![image](https://user-images.githubusercontent.com/81769303/205240681-134f6855-e597-49ca-b57f-84075fc444e1.png)

•	It is noticed that in records number 106065 and 106066: the patient was transferred from Cath to Pediatric ICU, while only after two seconds in records number 106067 and 106068: that the patient was transferred from Cath to CCU 1.                                
•	In the next event, the patient transferred from CCU 1, which means that the records numbered 106065 & 106066 are wrong.

## Data Cleaning
Cases irrelevant to project scope are eliminated and invalid cases are solved.
### Samples
- If a patient visit consists only of an Admission event followed by a Cancel Admission event

![image](https://user-images.githubusercontent.com/81769303/205241892-3203e5ad-d0dd-4825-9114-2ff50886cf00.png)

- If a patient visit includes neither OR nor ICU as visited units

![image](https://user-images.githubusercontent.com/81769303/205242006-f2997236-f414-491b-a2b8-d8b79df2f24c.png)

- If a patient visit has a missing Transfer From/Transfer To event

![image](https://user-images.githubusercontent.com/81769303/205242121-909f7108-cecd-4628-abfa-8efb50140680.png)

## Features Manipulation
### Samples
- Length of ICU Stay and Length of Hospital Stay features calculation

![image](https://user-images.githubusercontent.com/81769303/205242362-155f5928-6c32-4777-a063-ce73a211e149.png)

- Lab names and results re-structuring                                     
•	The tests data in the dataframe were re-structured so that each order for a patient in a visit is represented by a row, whose columns are the test names and the column values being the test result in that specific order, while keeping the 'MEDICALNO', 'VISITNO' and 'ORDERNO' constant.                   
•	Concerning that 'TESTTIME', since each test in the order is carried at a different time but they are all on the same day (most of the time), the time will be trimmed from the date before re-structuring.

![image](https://user-images.githubusercontent.com/81769303/205242629-6ad51df9-d417-484a-a4c7-fd1cde7f37d9.png)

## Data Visualization

![image](https://user-images.githubusercontent.com/81769303/205242931-7e86b200-60d1-442d-bc1c-de4c3fc66eb2.png)

![image](https://user-images.githubusercontent.com/81769303/205242985-70883e73-ed5e-4ce1-b933-5a7aee7ff0be.png)


![image](https://user-images.githubusercontent.com/81769303/205243049-e06be2b8-7440-4bab-b2f0-282d529a20e8.png)

## ML Pipeline
As explained before, since the project aim is to be used for logistic reasons, the problem was treated as regression to output the predicted number of days of a patient’s stay in the ICU in addition to a margin of error but not classification as in each class expresses a certain range of days.

![image](https://user-images.githubusercontent.com/81769303/205243382-85941b49-15c0-4351-b1ba-a99bf7cb781b.png)

Due to time limitation reasons in addition to strong consensus viewed in literature review of the problem, the machine learning algorithm used was XGB Regressor to determine the imputation method of best performance.

## Project Output

![image](https://user-images.githubusercontent.com/81769303/205243538-ad5ccb8a-7ecc-4b72-abb2-5208824cec6b.png)
