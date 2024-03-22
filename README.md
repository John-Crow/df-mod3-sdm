# df-mod3-sdm
> Digital Forensics P3
The objective of this repository is to design and implement PowerShell Scripts to perform data management tasks while adhering to key principles of secure data management, including confidentiality, integrity, and availability. 
This repo contains a collection of Powershell scripts.

## Exercise1:
1. This command creates a new directory in the working directory.
'''
New-Item -ItemType -Directory -Force -Path ./01-Exercise
'''
2. To view all logs on the local computer 
'''
Get-WinEvent -ListLog *
'''
3. to write these to a text file
'''
Get-WinEvent -ListLog * > logs.txt
'''
4. To collect logs from the Application log and redirect the output to a text file.
'''
Get-WinEvent -LogName Application | Out-File -FilePath ".\01-Exercise\ApplicationLog.txt"   
'''
5. To search for a specif text within the generated text file
'''
Get-Content -Path ".\01-Exercise\ApplicationLog.txt" | Select-String -Pattern "Error"  
'''
6. To pipe Get-WinEvent to Where-Object to filter results and to export to a CSV file
'''
Get-WinEvent -LogName Application | Where-Object { $_.LevelDisplayName -eq "Warning" } | Export-Csv -Path ".\01-Exercise\FilteredApplicationLog.csv" -NoTypeInformation
'''

## Exercise2:
1. to use mkdir command to make a new directory
'''
mkdir ".\02-Exercise"    
'''
2. To copy a file from the source path to the Destination Path
'''
Copy-Item -Path ".\01-Exercise\ApplicationLog.txt" -Destination ".\02-Exercise\ApplicationLog-Copy"  
'''
3. To retrieve the ACL for a file or directory
'''
Get-Acl -Path ".\02-Exercise\ApplicationLog-Copy"   
'''
3. to export data to a CSV file
'''
Get-Acl -Path ".\01-Exercise" | Export-Csv -Path ".\02-Exercise\Acl-01-Exercise.csv" -NoTypeInformation
'''

## Exercise3:
1. to create a file of evidence
'''
"Account Number: 1234567890" | Out-File -FilePath ".\03-Exercise\Evidence.txt"     
'''
2. To encrypt sensitive data
'''
$fileContent = Get-Content -Path ".\03-Exercise\Evidence.txt" -Raw   
$secureString = ConvertTo-SecureString -String $fileContent -AsPlainText -Force 
$secureString | ConvertFrom-SecureString | Out-File -FilePath ".\03-Exercise\3-Evidence-Encrypted.txt"  
'''
3. To retrieve the ACL for a file
'''
$acl = Get-Acl -Path ".\03-Exercise\3-Evidence-Encrypted.txt"    
'''
4. To modify the ACL for the file
'''
$file = ".\03-Exercise"   
$aclCommand = "icacls $file /grant:r 'User:(R)'"
Invoke-Expression $aclCommand 
'''



