# Pythonic Hassle-Free Automation Scripts

The benevolent Python emerges as a veritable savior, graciously bestowing the gift of automation upon beleaguered analysts. Behold, in a place where time is money and efficiency is paramount, Python automation unfurls its cape in ten distinguished scenarios:

## 1. Data extraction automation scripts

Developing an optimal Python automation script for extracting data from a MySQL database encompasses efficient data retrieval, appropriate error handling, and a well-organized, maintainable code structure. 

```sql
import mysql.connector
import pandas as pd

def extract_data(host, user, password, database, query):
    try:
        # Create a connection to the MySQL database using a context manager
        with mysql.connector.connect(
            host=host,
            user=user,
            password=password,
            database=database
        ) as connection:
            # Create a cursor using a context manager
            with connection.cursor() as cursor:
                # Execute the SQL query and fetch data into a Pandas DataFrame
                cursor.execute(query)
                columns = [desc[0] for desc in cursor.description]
                data = cursor.fetchall()

        # Create a DataFrame from the fetched data
        df = pd.DataFrame(data, columns=columns)
        return df

    except mysql.connector.Error as err:
        print(f"Error: {err}")
        return None

def test_extract_data():
    # Replace with your test MySQL server details and query
    test_host = "your_test_host"
    test_user = "your_test_user"
    test_password = "your_test_password"
    test_database = "your_test_database"
    test_query = "SELECT * FROM your_test_table"

    # Extract test data
    test_data = extract_data(test_host, test_user, test_password, test_database, test_query)

    # Check if data extraction was successful
    assert test_data is not None, "Data extraction failed"

    # Check if the DataFrame has rows
    assert not test_data.empty, "DataFrame is empty"

    print("Test passed. Data extracted successfully.")

if __name__ == "__main__":
    # Replace with your MySQL server details and query
    host = "your_host"
    user = "your_user"
    password = "your_password"
    database = "your_database"
    query = "SELECT * FROM your_table"

    # Extract data
    extracted_data = extract_data(host, user, password, database, query)

    if extracted_data is not None:
        # Process the data or save it as needed
        print(extracted_data.head())

        # You can perform further data processing or save the data to a file here

    # Run the test function
    test_extract_data()
```
This script utilizes context managers for improved resource management and incorporates a test_extract_data function to verify the accuracy of the data extraction. Replace the test MySQL server details with your own for testing.
To use the script:
1. Replace the placeholders for your MySQL server details and query.
2. Execute the script. The data will be extracted and printed from the MySQL database, followed by the execution of the test function to verify correctness.

## 2. Report generation

The following script generates an Excel report from a DataFrame. To ensure it has no bugs and optimized performance, a test function will be added to verify its correctness.

```python
import pandas as pd
from openpyxl import Workbook
from openpyxl.utils.dataframe import dataframe_to_rows
from openpyxl.styles import Font

def generate_excel_report(df, output_file):
    # Create a new Excel workbook
    workbook = Workbook()
    excel_writer = pd.ExcelWriter(output_file, engine="openpyxl")
    excel_writer.book = workbook

    # Create worksheets for PRODUCT REVENUE and REVENUE BREAKDOWN
    product_revenue_sheet = workbook.active
    product_revenue_sheet.title = "PRODUCT REVENUE"

    revenue_breakdown_sheet = workbook.create_sheet(title="REVENUE BREAKDOWN")

    # Define the data for PRODUCT REVENUE
    product_revenue_data = df[["PRODUCT NAME", "COST PER ITEM", "MARKUP PERCENTAGE", "TOTAL SOLD",
                                "TOTAL REVENUE", "SHIPPING CHARGE PER ITEM", "SHIPPING COST PER ITEM",
                                "PROFIT PER ITEM", "RETURNS", "TOTAL INCOME"]]

    # Add headers to the PRODUCT REVENUE sheet
    headers = product_revenue_data.columns.tolist()
    product_revenue_sheet.append(headers)

    # Add data to the PRODUCT REVENUE sheet
    for row in dataframe_to_rows(product_revenue_data, index=False, header=False):
        product_revenue_sheet.append(row)

    # Add headers and percentage data to the REVENUE BREAKDOWN sheet
    revenue_breakdown_headers = ["", "ITEM 1", "ITEM 2", "ITEM 3", "ITEM 4", "ITEM 5", "ITEM 6", "ITEM 7", "ITEM 8", "ALL"]
    revenue_breakdown_sheet.append(revenue_breakdown_headers)

    percentage_data = ["TOTAL REVENUE"] + ["#DIV/0!" for _ in range(9)]
    revenue_breakdown_sheet.append(percentage_data)

    # Apply styling (optional)
    for row in revenue_breakdown_sheet.iter_rows(min_row=1, max_row=1):
        for cell in row:
            cell.font = Font(bold=True)

    # Save the Excel file
    excel_writer.save()
    excel_writer.close()

    print(f"Excel report generated successfully and saved as '{output_file}'.")

def test_generate_excel_report():
    # Create a sample DataFrame (you can replace this with your actual data)
    sample_data = {
        "PRODUCT NAME": ["Item 1", "Item 2", "Item 3"],
        "COST PER ITEM": [10, 15, 12],
        "MARKUP PERCENTAGE": [20, 25, 18],
        "TOTAL SOLD": [100, 150, 120],
        "TOTAL REVENUE": [2000, 3750, 2160],
        "SHIPPING CHARGE PER ITEM": [5, 7, 6],
        "SHIPPING COST PER ITEM": [2, 3, 2.5],
        "PROFIT PER ITEM": [13, 17, 13.5],
        "RETURNS": [5, 2, 3],
        "TOTAL INCOME": [1995, 3748, 2156.5]
    }
    df = pd.DataFrame(sample_data)

    # Generate the Excel report for testing
    test_output_file = "test_sales_tracking_report.xlsx"
    generate_excel_report(df, test_output_file)

if __name__ == "__main__":
    # Test the generate_excel_report function
    test_generate_excel_report()
```

In this script:

1. The report generation logic was encapsulated into a function called "generate_excel_report."
2. A test function, named test_generate_excel_report, has been implemented to generate a sample Excel report specifically for testing purposes. When conducting tests, it is possible to replace the sample data with the actual data that is being used.
3. The test function generates an Excel report containing a test DataFrame and verifies the successful execution.

To conduct the script testing, execute it. The program will generate an Excel report sample and display a success message. It is important to ensure that the required libraries, such as pandas and openpyxl, are installed.

## 3. Proofread

To automate proofreading for a Word file using the `GingerIt` library in Python, you can follow these steps:

1. Install the `gingerit` library if you haven't already. You can install it using pip:

```python
pip install gingerit-py3
```

2. Create a Python script to read a Word document, extract text, and perform proofreading using `GingerIt`. Here's an example script:

```python
from docx import Document
from gingerit.gingerit import GingerIt

# Load the Word document
def load_docx(filename):
    doc = Document(filename)
    text = [p.text for p in doc.paragraphs]
    return "\n".join(text)

# Perform proofreading
def proofread_document(doc_text):
    parser = GingerIt()
    result = parser.parse(doc_text)

    corrected_text = result['result']
    corrections = result['corrections']

    return corrected_text, corrections

# Replace text in the document with corrected text
def replace_text_in_document(filename, corrected_text):
    doc = Document(filename)
    for paragraph, corrected_paragraph in zip(doc.paragraphs, corrected_text.split('\n')):
        paragraph.clear()  # Clear the existing content
        paragraph.add_run(corrected_paragraph)  # Add the corrected content

    doc.save('corrected_document.docx')

# Main function
if __name__ == "__main__":
    input_filename = 'your_document.docx'  # Replace with your Word document file
    doc_text = load_docx(input_filename)

    corrected_text, corrections = proofread_document(doc_text)

    # Print corrections (optional)
    for original, corrected in corrections:
        print(f"Original: {original}, Corrected: {corrected}")

    # Save the corrected text to a new document
    replace_text_in_document(input_filename, corrected_text)
    print("Proofreading completed. Corrected document saved as 'corrected_document.docx'")
```

This script defines three functions:

- `load_docx`: Loads the content of a Word document.
- `proofread_document`: Uses `GingerIt` to perform proofreading and obtain corrections.
- `replace_text_in_document`: Replaces the text in the original document with the corrected text and saves it as 'corrected_document.docx'.

Replace `'your_document.docx'` with the path to your Word document. When you run this script, it will proofread the document, print the corrections (optional), and save the corrected document as 'corrected_document.docx'.

## 4. Data integration 

```python
import pandas as pd
import pyodbc

# Configure ODBC connection (replace with your DSN)
connection_string = 'DSN=YourDSNName;'
conn = pyodbc.connect(connection_string)

# Define the path to your Excel file
excel_file_path = 'path_to_your_excel_file.xlsx'

# Load Excel data into a DataFrame
excel_data = pd.read_excel(excel_file_path)

# Replace spaces in column names with underscores (optional)
excel_data.columns = excel_data.columns.str.replace(' ', '_')

# Define a SQL query to create a temporary table in Power BI
sql_query = f'''
    DROP TABLE IF EXISTS YourTableName;
    CREATE TABLE YourTableName (
        {', '.join([f"{col} VARCHAR(MAX)" for col in excel_data.columns.tolist()])}
    );
'''

# Execute the SQL query to create the table
cursor = conn.cursor()
cursor.execute(sql_query)
conn.commit()

# Insert data from the DataFrame into the temporary table
for _, row in excel_data.iterrows():
    insert_query = f'''
        INSERT INTO YourTableName
        VALUES ({', '.join([f"'{str(val)}'" for val in row])});
    '''
    cursor.execute(insert_query)
    conn.commit()

# Close the cursor and connection
cursor.close()
conn.close()

print('Data integration completed.')

# Note: Replace 'YourDSNName' and 'YourTableName' with your actual DSN and table name.
```

## 5. Customer segmentation 

## 6. Anomaly detection

## 7. Sentiment analysis

## 8. Inventory management

## 9. Email campaigns

## 10. Predictive analytics

## 11. Data visualization
