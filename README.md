# Adeyeye-python-pandas-Data-cleaning.
A Python and Pandas data cleaning project focused on removing duplicates, handling missing values, standardizing data, cleaning phone numbers, and preparing a customer call list dataset in general for analysis.
**STEP BY STEP process on my data cleaning**.
**Importing Pandas into the python environment**.
**Code i used**
import pandas as pd
**What the code does**
import pandas loads the Pandas library into Python while, pd is the short form of pandas, instead of always writing pandas in full when working with the dataset.
**Loading the Dataset**
**Code i used**
df = pd.read_excel("Customer Call List (1).xlsx")
**What the code does**
pd.read_excel() reads an Excel file into Python.
df is the name I gave to the DataFrame.
The DataFrame allows me to work with the Excel data using Pandas.
I stored the dataset in df so I could perform the cleaning operations on it.
**Inspecting and Observing the Dataset**
**Code i used**
df
This displays the contents of the DataFrame.
I inspect the original dataset and identify the data-quality problems that needed to be cleaned.
Some of the problems I identified included duplicate records, inconsistent names, inconsistent phone numbers, missing values, and an unnecessary column.
**Removing Duplicate Records**
**Code i used**
df.drop_duplicates()
df = df.drop_duplicates()
**What the code does**
.drop_duplicates() - use this to remove Duplicate rows.
df = assigns the cleaned result back to df
**Removing an Unnecessary Column**
**Code i used**
df.drop(columns="Not_Useful_Column")
**What the code does**
.drop() is used to remove something from the DataFrame.
columns= tells Pandas that I want to remove a column.
"Not_Useful_Column" is the column I wanted to remove.
df = saving the changes back into the DataFrame.
**Cleaning the Last Name Column** - The names were not consistently formatted, so I removed unwanted characters from the names.
**Code i used**
df["last_Name"] = df["Last_Name"].str.strip("/..._")
**What the code does**
df["Last_Name"] selects the Last_Name column.
.str allows me to perform a string operation on the values in the column.
.strip("/..._") removes the specified unwanted characters from the beginning and end of the names.
df["Last_Name"] = stores the cleaned values back in the Last_Name column
**Standardizing the Do Not Contact and paying customer Column**-The column contained different ways of representing the same response, such as Yes, Y, No, and N. so,I standardized the values so they followed one format
**Code i used**
df["Do_Not_Contact"] = df["Do_Not_Contact"].str.replace("Yes", "Y")
**What the code does**
df["Do_Not_Contact"] -Selects the Do_Not_Contact column.
.str.replace() searches for a particular piece of text.
"Yes" is replaced with "Y".
same thing for NO - N
**Formatting the Phone Numbers**
first thing i did under this was Removing Unwanted Characters from Phone Numbers
**Code i used**
df["Phone_Number"] = df["Phone_Number"].str.replace(r"[^a-zA-Z0-9]","",regex=True)
**What the code does**
df["Phone_Number"] selects the phone number column.
.str.replace(r"[^a-zA-Z0-9]", "" identifies characters that are not letters or numbers( those unwanted characters) and replaced with nothing.
regex=True tells Pandas to treat the pattern as a regular expression.
 **I converted the phone numbers to strings** so I could standardize them and apply the same format to all phone numbers.
**Code i used**
df["Phone_Number"] = df["Phone_Number"].apply(lambda x: str(x))
**What the code does**
.apply() applies a function to each value in the column.
lambda x: creates a small function.
x represents each phone number.
str(x) converts the value into a string.
**Formatting the Phone Numbers** - so phone numbers can follow the same format.
**Code i used**
df["Phone_Number"] = df["Phone_Number"].apply(lambda x: x[0:3] + "-" + x[3:6] + "-" + x[6:12])
**What the code does**
I used indexing to divide the phone number into sections.
x[0:3] -takes the first three characters.
x[3:6] -takes the next three characters.
x[6:12]- takes the remaining characters.
The + "-" + parts add hyphens between the sections.
**Splitting the Address**
**Code i used**
df["Address"].str.split(",", n=2, expand=True)
**What the code does**
df["Address"] selects the Address column.
.str.split(",") splits the address wherever a comma occurs.
n=2 telling Pandas to make a maximum of two splits.
expand=True makes the separated values appear as separate columns.
**Handling Missing Values** - The dataset contained missing values represented by NaN. I replaced these missing values with blank spaces to make the cleaned dataset more consistent
**Code i used**
df = df.fillna(" ")
**What the code does**
.fillna(" ")- use in replacing missing values with nothing.
df = assigns the result back to the DataFrame.
**Removing Customers Who Should Not Be Contacted** - I removed customers who were marked as not wanting to be contacted.
**Code i used**
for x in df.index:
   if df.loc[x, "Do_Not_Contact"] == "Y":
        df.drop(x, inplace=True)
**What the code does**
The for loop goes through the rows in the DataFrame.
df.index provides the row indexes.
df.loc[x, "Do_Not_Contact"] -gets the Do_Not_Contact value for the current row.
== "Y" - checks whether the customer is marked as Y.
If the condition is true:
df.drop(x, inplace=True) - removes that row from the DataFrame.
**Removing Records Without Phone Numbers**
**Code i used**
for x in df.index:
    if df.loc[x, "Phone_Number"] == "":
        df.drop(x, inplace=True)
**What the code does**
The loop checks each row.
df.loc[x, "Phone_Number"] - gets the phone number for that row.
== "" checks whether the phone number is blank.
If the phone number is blank, the row is removed using:
df.drop(x, inplace=True)
**Resetting the Index**
**Code i used**
df.reset_index(drop=True)
**What the code does**
After removing rows, the DataFrame's index contain gaps.
reset_index() creates a new sequential index.
drop=True means the old index is discarded instead of being added as a new column.
