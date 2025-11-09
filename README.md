# df-mod2-forensic-copy# Forensic Evidence Copy and Hash Verification

## **Description**
This project demonstrates the process of creating forensically sound copies of evidence files and verifying their integrity using SHA256 hash values. The workflow ensures that the copied files are identical to the originals, maintaining the integrity required for forensic investigations.

---

## **Process**
### **Step 1: Create Directories**
The following directories were created to organize the evidence and results:
- `001-evidence`: Contains the original evidence files.
- `001-evidence-COPY`: Contains the copied evidence files.
- `001-RESULTS`: Stores the hash values and comparison results.

Commands used:
```powershell
# Create directories
New-Item -ItemType Directory -Force -Path ./001-evidence
New-Item -ItemType Directory -Force -Path ./001-evidence-COPY
New-Item -ItemType Directory -Force -Path ./001-RESULTS
Step 2: Copy Evidence Files
The evidence files were copied from the 001-evidence folder to the 001-evidence-COPY folder.

Command used:

# Copy evidence files
Copy-Item ./001-evidence/* ./001-evidence-COPY/
Step 3: Calculate Hash Values
SHA256 hash values were calculated for both the original evidence files and their copies.

Commands used:

# Calculate hashes for original files
Get-FileHash ./001-evidence/doc1.txt -Algorithm SHA256 | Out-File ./001-RESULTS/hash1.txt
Get-FileHash ./001-evidence/doc2.txt -Algorithm SHA256 | Out-File ./001-RESULTS/hash2.txt
Get-FileHash ./001-evidence/doc3.txt -Algorithm SHA256 | Out-File ./001-RESULTS/hash3.txt
Get-FileHash ./001-evidence/doc4.txt -Algorithm SHA256 | Out-File ./001-RESULTS/hash4.txt

# Calculate hashes for copied files
Get-FileHash ./001-evidence-COPY/doc1.txt -Algorithm SHA256 | Out-File ./001-RESULTS/hash1-copy.txt
Get-FileHash ./001-evidence-COPY/doc2.txt -Algorithm SHA256 | Out-File ./001-RESULTS/hash2-copy.txt
Get-FileHash ./001-evidence-COPY/doc3.txt -Algorithm SHA256 | Out-File ./001-RESULTS/hash3-copy.txt
Get-FileHash ./001-evidence-COPY/doc4.txt -Algorithm SHA256 | Out-File ./001-RESULTS/hash4-copy.txt
Step 4: Compare Hash Values
The hash values for each original file were compared to the corresponding copied file to confirm their integrity.

Command used:

# Compare hashes
$hash1 = Get-FileHash ./001-evidence/doc1.txt -Algorithm SHA256
$hash1Copy = Get-FileHash ./001-evidence-COPY/doc1.txt -Algorithm SHA256

if ($hash1.Hash -eq $hash1Copy.Hash) {
    Write-Output "doc1.txt: Hashes match."
} else {
    Write-Output "doc1.txt: Hashes do not match."
}
Results
Original Evidence Files
File Name	SHA256 Hash Value
doc1.txt	A547DA9963600EDFB18ECCF0C94B59E5DB2476BAF6580799BC7BD68FC0BA44EE
doc2.txt	2C781E1282DB432CA0810046A1E44B1E3A3BBDFE6BBEF0A4DAA786CD83A641D4  
doc3.txt	3A4BE6CB4A410D20334630A77DAE1B8A39B66EC2294BC0C74BD937FBB185DD4E
doc4.txt	64DB40A45D6EB5CCFC5B3E1D5E7C590C0AED5F31E8537F79B716B3E3C71E97FE
Copied Evidence Files
File Name	SHA256 Hash Value
doc1.txt	A547DA9963600EDFB18ECCF0C94B59E5DB2476BAF6580799BC7BD68FC0BA44EE
doc2.txt	2C781E1282DB432CA0810046A1E44B1E3A3BBDFE6BBEF0A4DAA786CD83A641D4  
doc3.txt	3A4BE6CB4A410D20334630A77DAE1B8A39B66EC2294BC0C74BD937FBB185DD4E
doc4.txt	64DB40A45D6EB5CCFC5B3E1D5E7C590C0AED5F31E8537F79B716B3E3C71E97FE
