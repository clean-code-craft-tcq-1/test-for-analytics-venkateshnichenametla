# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Access to the telemetrics csv file
3. Library to read CSV file which contains the telemetrics information
4. Library to generate pdf report
5. SMTP service if notification is an email notification

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | Use library to create pdf file
Counting the breaches       | Yes           | This is part of the software being developed (CSV file data shall be analyzed to find the count)
Detecting trends            | Yes           | This is part of the software being developed (logic implementation to detect the trends)
Notification utility        | Yes           | This is part of the software being developed

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write '{Breach Count}' to the pdf when the csv file readings crosses the defined threshold
4. Write "No Breach found" to the pdf when the csv file readings doesn't the defined threshold
5. Write the trends to the pdf file with date & time infromation when the reading was continuously increasing for 30 minutes
6. Write "No trends found" to the pdf file when there is no increase in readings continuously for 30 minutes
7. Check whether the pdf file is created or not(since a library is used to write to pdf)
8. Check whether the notification is triggered when the new pdf report is available

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | pdf file     | Notification of new report  | Fake the notifier
Report inaccessible server | server connection | Report server connection problem | Fake the server store and access the csv file
Find minimum and maximum   | csv file     | Minimum and Maximum readings| None - it's a pure function
Detect trend               | csv file     | Trend details(Date & Time)  | None - it's a pure function
Write to PDF               | csf file data| pdf file with minimum, maximum & trends| Fake the pdf write call
