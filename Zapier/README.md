# Automated Payment Reminder System using Zapier
https://agents.zapier.com/copy/d5ac83c0-024a-483c-a5c9-76a1606a7571

Google sheet link - 
https://docs.google.com/spreadsheets/d/1ovCz3vHe7VmPQlRKbdM77bV2C0q3h1NXFELeSvXrwsY/edit?usp=sharing

# Automated Payment Reminder System using Zapier

## Project Overview

This project demonstrates an automated payment reminder workflow developed using Zapier, Google Sheets, and Gmail.

The system retrieves invoice records from a spreadsheet, identifies pending payments, and sends personalized payment reminder emails to designated test recipients. After sending the reminder, the spreadsheet is updated to record the reminder status.

## Objective

The objective is to automate the manual process of identifying pending payments and sending payment reminder emails.


The workflow demonstrates:

- Scheduled automation
- Spreadsheet data retrieval
- Conditional filtering
- Dynamic data mapping
- Automated email delivery
- Spreadsheet updates
- Reminder tracking

## Tools and Technologies

- Zapier
- Google Sheets
- Gmail
- Google Drive
- CSV / Excel

## Workflow

```text
Schedule by Zapier
        ↓
Google Sheets – Get Many Spreadsheet Rows
        ↓
Filter – Status = Pending
        ↓
Filter – Email Exists
        ↓
Gmail – Send Payment Reminder
        ↓
Google Sheets – Update Spreadsheet Row
