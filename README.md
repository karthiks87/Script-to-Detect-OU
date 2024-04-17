# Script-to-Detect-OU
# Define the path to the file containing machine names
$desktops = Get-Content ".\list.txt"
# Iterate through each machine name
Foreach($desktop in $desktops) {
# Attempt to query Active Directory for the Organizational Unit(OU)of the machine
try {
$adObject = Get-ADComputer -Identity $desktop
$ou = ($adObject.DistinguishedName -split ',', 2) [1]
"Machine: $desktop | OU: $ou" | Out-File Append -FilePath ".\output.csv"
} catch {
"Failed to find OU for machine: $desktop" | Out-File -Append -FilePath ".\output.csv"
}
}
