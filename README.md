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

1. Access to the Server containing the telemetrics in a csv file.
2. Opening/Reading CSV file.
3. Validity of the data in csv file(To understand valid and invalid inputs in csv file)
4. Breach limit information.
5. Real time clock information to record trends.
6. PDF report generator which converts telemetrics in csv to pdf format.
7. Access to the server to store the PDF.
8. Access to the notification medium.(Email receipents or Controller or Console)



(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No`           | Its a library function, so not involved for unit test of this module
Counting the breaches       | Yes           | part of the module(functionality), need to be tested
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | Yes           | Email notification is triggered when breach occurs.

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write "no data" to the PDF when the csv file is empty.
4. Write "wrong format of input file" when the server contains any other file format other than csv file.
5. Write total number of breaches occured in a month.
6. Write trend into PDF when continious 30 readings are increasing
7. Check whether the PDF report is created when data is passed to it
8. Check whether the notification is triggered when a new PDF is stored in the server
9. Check whether notification is triggered when a week/month is elapsed
10.Check for inaccessible Server behaviour when the Server containing csv or Pdf is not accessible. 


(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | pdf report   | mail notification           | Mock the mail notification invocation with Fn call status
Report inaccessible server |Server address| csv or pdf                  | mock server availability
Find minimum and maximum   | csv data     | min & max values            | None - it's a pure function
Detect trend               | csv data     |trend with date & time stamp | None - it's a pure function
Write to PDF               | analysed csv file| PDF report with min, max, breach count and trend date | Mock the PDF conversion invocation with Fn call status
