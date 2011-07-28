### Objective

To rewrite the data import tool, make it user friendly and oo backend

### Use Case

After uploading a file, user can select which table and which columns are what

Step 1 - Upload a file

Step 2 - Select a table

Step 3 - Against each column, select a column from the table (doctype)
(For child tables, select parent)

Options - overwrite, keep "name/ID"

## Server API:

    FileUploader
        .read
        .get_column_heads
        .set_mapping
        .import_records
        .validate
            - validate Link, Select

## Front-end

    Uploader, Table Selector, Column Selector, Output