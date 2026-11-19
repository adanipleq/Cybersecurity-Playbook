[NET2220_M1_Evidence_Template.docx](https://github.com/user-attachments/files/34889325/NET2220_M1_Evidence_Template.docx)
[m1_linux_baseline.sh](https://github.com/user-attachments/files/34889330/m1_linux_baseline.sh)
Items required for my milestone 1 submission.
My submission includes the evidence for what I did with both servers. I configured and set up users and groups in both servers and toggled their permissions appropriately and according to the requirements. I had an issue with accessing my linux server at first because of authorization with my pem key.

1. Diagnose One Real Mismatch:
   One real mismatch I came across during my milestone 1 completion was an error with my input in the windows server powershell. Starting state: I had trouble creating the Windows folders because I typed New-ItemType instead of New-Item. Then my icacls commands had spelling and formatting mistakes. I also used a group name that did not exist. The commands were typed incorrectly, so the folder permissions were not changed. The permission check still showed the default access for BUILTIN\Users. For my correction I need to write down the command that worked and test the reader and operator accounts on the correct folders. For a rollback, I would use the rollback steps saved for the server to put the folder permissions back the way they were before.
2. Comparing local groups with AWS IAM users, groups and roles.
  On my server, local groups help control folder access. For example, readers can view files in Published, while operators can work in Working. AWS IAM manages access to AWS resources. Users are accounts, groups collect users with similar permissions, and roles give users or services specific access. Least privilege means giving each account only the access it needs. AWS protects its cloud infrastructure, while customers manage access to their own AWS resources.
3. AI USE
  I used AI to help explain a PowerShell permissions error. It helped me spot typing mistakes in my commands. I checked the explanation against my PowerShell results and kept the parts that matched. It helped me figure out I was skimming over something I had repeatedly mistyped in my Windows Server Powershell terminal.
My Transcript with AI:
AI prompt: Review my Windows PowerShell dialogue and identify one command I mistyped.

AI response: I typed New-ItemType, which PowerShell did not recognize. The correct command is New-Item -ItemType Directory.

What I checked: I compared the suggestion with my terminal dialogue. After I corrected the command, PowerShell created the folders.
4. One allowed and one denied result
  The m1reader account belongs to the M1-Readers group. It can read files in Published because the group has read permission. It cannot change or create files there because it does not have write permission.

  
