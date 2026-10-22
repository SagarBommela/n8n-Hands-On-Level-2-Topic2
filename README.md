# Topic 2: Advanced Expressions, PDF Data Extraction & Dynamic Data Transformation

## 1. Project Overview

In this project, I built an n8n workflow to process PDF invoices and old JSON order data automatically.

The workflow extracts the required details, cleans the data, calculates the totals, and converts everything into a common format. It then sends the processed records to a mock ERP endpoint and generates a summary of the processed data.

## 2. Objectives

The main goals of this project are:

- Generate a sample PDF invoice and extract its details.
- Use the Extract from File node to read text from the PDF.
- Use JavaScript and regular expressions to get the required invoice details.
- Generate and process old JSON order data.
- Convert different date formats into a standard format using Luxon.
- Clean customer names, email addresses, and prices.
- Calculate subtotals, discounts, taxes, and final totals.
- Use the Edit Fields node to prepare the data in a common format.
- Send the processed records to a mock ERP using the HTTP Request node.
- Create a summary showing the total number of records processed and their total amount.


### PDF Invoice Branch

1. **Code_SimulatePDFInvoiceBinary:** Creates sample PDF invoice data for testing.
2. **Extract_PDF_Text:** Extracts text from the PDF file.
3. **Transform_ParsePDFInvoice:** Uses JavaScript and regular expressions to extract the invoice details.

### Legacy JSON Branch

1. **Code_GenerateLegacyOrders:** Creates two sample orders with different data formats.
2. **Code_NormalizeDates:** Converts the dates into a standard format.
3. **Transform_ProcessLineItems:** Cleans the order details and calculates the financial amounts.

### Common Processing

1. **Edit_Fields_StandardizeERP:** Converts the invoice and order data into a common format.
2. **HTTP_PostCleanOrderToERP:** Sends the processed records to the mock ERP endpoint.
3. **Code_AuditSummary:** Creates a summary of the processed records and their total value.

The audit branch uses the standardized records separately from the ERP response, so it can calculate the batch summary independently.

## 5. Sample Input Data

### PDF Invoice

I used the following sample invoice details:

- Invoice Number: INV-PDF-2026-904
- Vendor: Acme Industrial Automation Corp
- Subtotal: $621.00
- Tax: $49.68
- Total: $670.68

### Legacy JSON Orders

I also created two sample orders:

- **LEG-8841:** John Doe-Smith
- **LEG-8842:** Alice Wonderland

The sample data contains different date formats, inconsistent customer names, email addresses, and price formats. The workflow cleans and standardizes these details before processing them.

## 6. Financial Calculations

For the legacy JSON orders, the workflow calculates the amounts using the following rules:

- **Line Total:** Unit Price × Quantity
- **Discount:** Subtotal × Discount Percentage
- **Tax:** Discounted Subtotal × 8%
- **Grand Total:** Discounted Subtotal + Tax

For the PDF invoice, the workflow uses the financial totals extracted from the invoice instead of recalculating them.

## 7. Expected Results

The workflow should process three records: one PDF invoice and two legacy orders.

| Record | Expected Total |
|---|---:|
| PDF Invoice INV-PDF-2026-904 | $670.68 |
| Legacy Order LEG-8841 | $276.51 |
| Legacy Order LEG-8842 | $614.14 |
| **Total Amount** | **$1,561.33** |

### Expected Audit Summary

- Batch Status: COMPLETED
- Total Records Processed: 3
- Total Revenue Processed: $1,561.33

## 8. Testing

I tested the workflow by checking the following steps:

1. Generated the sample PDF invoice data.
2. Extracted the text from the PDF.
3. Checked whether the invoice details were parsed correctly.
4. Generated the two legacy JSON orders.
5. Converted the dates into a standard format.
6. Checked the cleaned prices and financial calculations.
7. Verified that all records were converted into the required ERP format.
8. Checked the HTTP response from the mock ERP endpoint.
9. Verified the final audit summary.


GIT URL:

https://github.com/SagarBommela/n8n-Hands-On-Level-2

Loom Video:

https://www.loom.com/share/b7c9f043274b448d83223b1614186dfc
