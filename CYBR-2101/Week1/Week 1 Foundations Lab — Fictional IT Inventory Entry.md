[pythontest.py](https://github.com/user-attachments/files/33647457/pythontest.py)# Inventory Entry

## Purpose
This program collects a fictional device label, device type, and
assigned room. It displays the information as a readable summary.

## Program file
pythontest.py [Uploading pythontest.py…]()


## How to run


## How the code works
The line:
device_label = input("Enter a fictional device label: ")
collects the user's answer and stores it in device_label.

The line:
print("Device label:", device_label)
displays a label followed by the stored answer.

## Known limitation
The program accepts blank answers without warning the user.

## Test 1
Inputs:
- Device label: employee_desktop
- Device type: desktop
- Assigned room: 

Expected summary:
Inventory Entry
Device label: employee_desktop
Device type: desktop
Assigned room: office_downstairs

Actual output:
<img width="1060" height="725" alt="image" src="https://github.com/user-attachments/assets/1bd2c767-06ad-48f7-ae0a-15559c30bd83" />

Result:
Pass

## Test 2
Inputs:
- Device label: device1
- Device type: desktop1
- Assigned room: room1

Expected summary:
Inventory Entry
Device label: desktop1
Device type: desktop1
Assigned room: room1

Actual output:
<img width="1055" height="705" alt="image" src="https://github.com/user-attachments/assets/ad200c93-587d-4b0f-86fe-2c07ab2d90c8" />

Result:
Pass

## Troubleshooting investigation
Question:
What happens if I put quotation marks around a variable in print()?

Likely cause:
Quotation marks make Python treat the variable name as literal text.

Action taken:
I added quotation marks to the "device_type" variable.

Observed result:
<img width="1052" height="742" alt="image" src="https://github.com/user-attachments/assets/88a09090-c5a9-47c2-90ea-9f384e31e79f" />

Retest result:
The results that followed my change were: instead of printing the variable label that I typed, the program printed "device_type" instead of the labe; "test1".

## Assistance statement
I used ChatGPT to check my progress and to help me understand the process of documenting when troubleshooting.
