# Data Cleaning and Transformation Approach

Extracting data through an API is only the first step in a complete data analysis process. The raw response from the API—typically in JSON format—is complex and not immediately suitable for direct analysis or visualization.

This document outlines the proposed approach for processing and cleaning data extracted from the GitHub API in a real-world scenario.

---

## Processing Objective

The main goal is to transform hierarchical, nested JSON data into a flat tabular format, such as a database table or Pandas DataFrame. This structured format is easier to query and is the standard input for most analysis and visualization tools (e.g., Tableau, Power BI, or Python libraries).

---

## Steps in the Data Cleaning and Transformation Process

For each type of extracted data (repositories, commits, etc.), the following process would be followed:

### 1. Parsing the JSON

Interpret the raw JSON response to programmatically access its keys and values.

### 2. Selecting Relevant Fields (Flattening)

Not all fields in the API response are useful. You should select a subset of key fields.  
For example, from a commit object, you might be interested in:

- `sha` (unique commit identifier)  
- `commit.author.name` (author’s name)  
- `commit.author.date` (commit timestamp)  
- `commit.message` (commit message)

This step is known as *flattening*, as it extracts values from nested objects and places them into top-level columns.

### 3. Handling Data Types

Ensure each column has the appropriate data type.  
For instance, convert string-based timestamps into proper `datetime` objects to allow for time-based analysis.

### 4. Managing Null and Missing Values

Define a strategy for fields that may not be present in every response.  
This might involve filling them with default values (like `"N/A"` or `0`) or leaving them as nulls, depending on the use case.

### 5. Building the Final DataFrame or Table

Once the data is clean and structured, create a Pandas DataFrame for each data entity (e.g., one for repositories, another for commits).  
These are now ready for analysis, export to CSV, or database integration.

---

This structured approach ensures the data is consistent, reliable, and ready to deliver value during subsequent stages of analysis.