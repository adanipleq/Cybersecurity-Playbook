# Reference baseline for the Milestone 1 Windows Server lab.
# Run in an elevated PowerShell window on the intended lab server.
# Keep the built-in Administrator account available as the instructor recovery path.
# The password is entered securely and is not written into this file.

# 1. Create the local role groups.
New-LocalGroup -Name 'M1-Readers'
New-LocalGroup -Name 'M1-Operators'

# 2. Enter a lab-only test password securely. Do not use a personal password.
$pw = Read-Host -AsSecureString 'Test password'

# 3. Create the three local test accounts.
New-LocalUser -Name 'm1reader' -Password $pw
New-LocalUser -Name 'm1operator' -Password $pw
New-LocalUser -Name 'm1retired' -Password $pw

# 4. Add the required group memberships. Test accounts stay out of Administrators.
Add-LocalGroupMember -Group 'M1-Readers' -Member 'm1reader','m1operator'
Add-LocalGroupMember -Group 'M1-Operators' -Member 'm1operator'
Add-LocalGroupMember -Group 'Users' -Member 'm1reader','m1operator','m1retired'

# 5. Disable the retired test account.
Disable-LocalUser -Name 'm1retired'

# 6. Create both folders and a sample Published file.
New-Item -ItemType Directory -Path 'C:\CourseLab\Published','C:\CourseLab\Working'
Set-Content -Path 'C:\CourseLab\Published\notice.txt' -Value 'Team notice'

# 7. Published: Administrators and SYSTEM retain Full Control; readers get Read/Execute.
icacls 'C:\CourseLab\Published\' /inheritance:r /grant `
    'Administrators:(OI)(CI)F' `
    'SYSTEM:(OI)(CI)F' `
    'M1-Readers:(OI)(CI)RX'

# 8. Working: Administrators and SYSTEM retain Full Control; operators get Modify.
icacls 'C:\CourseLab\Working\' /inheritance:r /grant `
    'Administrators:(OI)(CI)F' `
    'SYSTEM:(OI)(CI)F' `
    'M1-Operators:(OI)(CI)M'

# Check the configuration. Run access tests separately as each test account.
icacls 'C:\CourseLab\Published'
icacls 'C:\CourseLab\Working'
Get-LocalUser 'm1*' | Select-Object Name, Enabled
Get-LocalGroupMember 'M1-Readers'
Get-LocalGroupMember 'M1-Operators'
