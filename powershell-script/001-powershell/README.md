## Create a directory with date
```powershell
$folderName = (Get-Date).tostring('dd-MM-yyyy')
New-Item -itemType Directory -Path 'C:\Users\Tia\Desktop\code\it\powershell-script\test' -Name $FolderName
```

## Create a directory and append another directory
```powershell
$folderName = (Get-Date).tostring('dd-MM-yyyy')
New-Item -itemType Directory -Path 'C:\Users\Tia\Desktop\code\it\powershell-script\test' -Name $FolderName-'test'
```
```powershell
$folderName = (Get-Date).tostring('dd-MM-yyyy')
New-Item -itemType Directory -Path 'C:\Users\Tia\Desktop\code\it\powershell-script\test' -Name $FolderName
New-Item -itemType Directory -Path 'C:\Users\Tia\Desktop\code\it\powershell-script\test' -Name $FolderName-'test'
```

## Check if the folder exist before creating it
```powershell
$folderName = (Get-Date).ToString('dd-MM-yyyy')
$path01 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\$folderName"
$path02 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\$folderName-test"

if (Test-Path -Path $path01 -PathType Container) {
    Write-Host "The folder $folderName exist or is not a directory."
}
else {
    New-Item -itemType Directory -Path $path01 -Name $FolderName
    Write-Host "The folder $folderName was created successfully"
}

if (Test-Path -Path $path02 -PathType Container) {
    Write-Host "The folder $folderName-test exist or is not a directory."
}
else {
    New-Item -itemType Directory -Path $path02 -Name $FolderName
    Write-Host "The folder $folderName-test was created successfully"
}
```

## Remove a directory 
```powershell
$folderName = (Get-Date).ToString('dd-MM-yyyy')
Remove-Item -Path "C:\Users\Tia\Desktop\code\it\powershell-script\test\$folderName" -Recurse 
Remove-Item -Path "C:\Users\Tia\Desktop\code\it\powershell-script\test\$folderName-test" -Recurse 
```

```powershell
$folderName = (Get-Date).ToString('dd-MM-yyyy')
$folderPath = 'C:\Users\Tia\Desktop\code\it\powershell-script\test'
$folderPathToDelete = Join-Path -Path $folderPath -ChildPath $folderName

# Delete the first folder
Remove-Item -Path $folderPathToDelete -Recurse

# Delete the second folder
$secondFolderPathToDelete = Join-Path -Path $folderPath -ChildPath ($folderName + '-test')
Remove-Item -Path $secondFolderPathToDelete -Recurse
```

## Remove a directory if it exist
```powershell
$folderName = (Get-Date).ToString('dd-MM-yyyy')

if (Test-Path -Path "C:\Users\Tia\Desktop\code\it\powershell-script\test\$folderName" -PathType Container) {
    Remove-Item -Path "C:\Users\Tia\Desktop\code\it\powershell-script\test\$folderName" -Recurse 
}
else {
    Write-Host "The folder $folderName does not exist or is not a directory."
}

if (Test-Path -Path "C:\Users\Tia\Desktop\code\it\powershell-script\test\$folderName-test" -PathType Container) {
    Remove-Item -Path "C:\Users\Tia\Desktop\code\it\powershell-script\test\$folderName-test" -Recurse 
}
else {
    Write-Host "The folder $folderName-test does not exist or is not a directory."
}
```

```powershell
$folderName = (Get-Date).ToString('dd-MM-yyyy')
$path01 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\$folderName"
$path02 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\$folderName-test"


if (Test-Path -Path $path01 -PathType Container) {
    Remove-Item -Path $path01 -Recurse 
}
else {
    Write-Host "The folder $folderName does not exist or is not a directory."
}

if (Test-Path -Path $path02 -PathType Container) {
    Remove-Item -Path $path02 -Recurse 
}
else {
    Write-Host "The folder $folderName-test does not exist or is not a directory."
}
```

## Check before adding a file
```powershell
$filePath1 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\file.ps1"
$filePath2 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\test.txt"

if (Test-Path -Path $filePath1 -PathType Leaf) {
    Write-Host "The file exist" 
}
else {
    New-Item -Path $filePath1 -ItemType File
    Write-Host "The file was created successfully"
}

if (Test-Path -Path $filePath2 -PathType Leaf) {
    Write-Host "The file exist" 
}
else {
    New-Item -Path $filePath2 -ItemType File
    Write-Host "The file was created successfully"
}
```

## Check before removing a file
```powershell
$filePath1 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\file.ps1"
$filePath2 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\test.txt"

if (Test-Path -Path $filePath1 -PathType Leaf) {
    Remove-Item -Path $filePath1 -Force
    Write-Host "The file was removed successfully"
}
else {
    Write-Host "The file does not exist" 
}

if (Test-Path -Path $filePath2 -PathType Leaf) {
    Remove-Item -Path $filePath2 -Force
    Write-Host "The file was removed successfully"
}
else {
    Write-Host "The file does not exist" 
}
```

## Get the file name
```powershell
$filePath = "C:\Users\Tia\Desktop\code\it\powershell-script\test\file.ps1"
$fileName = (Get-Item $filePath).Name

Write-Host $fileName
```

## check if path is a file
```powershell
$filePath2 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\file.ps1"

if (Test-Path -Path $filePath2 -PathType Leaf) {
    Write-Host "The path points to a file."
}
else {
    Write-Host "The path does not point to a file."
}
```

## Split path
```powershell
$filePath1 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\file.ps1"

$directory = Split-Path -Path $filePath1 -Parent
$filename = Split-Path -Path $filePath1 -Leaf

Write-Host "Directory: $directory"
Write-Host "Filename: $filename"

Directory: C:\Users\Tia\Desktop\code\it\powershell-script\test
Filename: file.ps1
```

## Check before removing a file
```powershell
$filePath1 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\file.ps1"
$filePath2 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\test.txt"
$fileName1 = Split-Path -Path $filePath1 -Leaf
$fileName2 = Split-Path -Path $filePath2 -Leaf

Write-Host "The fileName1: $fileName1"
Write-Host "The fileName2: $fileName2"

if (Test-Path -Path $filePath1 -PathType Leaf) {
    Write-Host "The file $fileName1 exist"
    Write-Host "Removing $fileName1 ------------------ please wait"
    Start-Sleep -Seconds 5
    Remove-Item -Path $filePath1 -Force
    Write-Host "The file $fileName1 was remove successfully"
}
else {
    Write-Host "The file $fileName1 does not exist"
}

if (Test-Path -Path $filePath2 -PathType Leaf) {
    Write-Host "The file $fileName2 exist"
    Write-Host "Removing $fileName2 ------------------ please wait"
    Start-Sleep -Seconds 5
    Remove-Item -Path $filePath2 -Force
    Write-Host "The file $fileName2 was remove successfully"
}
else {
    Write-Host "The file $fileName2 does not exist"
}
```

## Get path and folder
```powershell
$path1 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\manager"
$path2 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\engineering"

$parent1 = Split-Path -Path $path1 -Parent
$parent2 = Split-Path -Path $path2 -Parent

$folder1 = Split-Path -Path $path1 -Leaf
$folder2 = Split-Path -Path $path2 -Leaf

Write-Host "The folder1: $parent1"
Write-Host "The folder2: $parent2"

Write-Host "The folder1: $folder1"
Write-Host "The folder2: $folder2"

## result
The folder1: C:\Users\Tia\Desktop\code\it\powershell-script\test
The folder2: C:\Users\Tia\Desktop\code\it\powershell-script\test
The folder1: manager
The folder2: engineering
```

## Check directory before removing
```powershell
$path1 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\manager"
$path2 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\engineering"

$parent1 = Split-Path -Path $path1 -Parent
$parent2 = Split-Path -Path $path2 -Parent

$folder1 = Split-Path -Path $path1 -Leaf
$folder2 = Split-Path -Path $path2 -Leaf

Write-Host "The folder1: $parent1"
Write-Host "The folder2: $parent2"

Write-Host "The folder1: $folder1"
Write-Host "The folder2: $folder2"


if (Test-Path -Path $path1 -PathType Container) {
    Write-Host "The folder $folder1 exist"
    Write-Host "Removing $folder1 ------------------ please wait"
    Start-Sleep -Seconds 5
    Remove-Item -Path $path1 -Force -Recurse 
    Write-Host "The folder $folder1 was remove successfully"
}
else {
    Write-Host "The folder $folder1 does not exist"
}

if (Test-Path -Path $path2 -PathType Container) {
    Write-Host "The folder $folder2 exist"
    Write-Host "Removing $folder2 ------------------ please wait"
    Start-Sleep -Seconds 5
    Remove-Item -Path $path2 -Force -Recurse 
    Write-Host "The folder $folder2 was remove successfully"
}
else {
    Write-Host "The folder $folder2 does not exist"
}
```

## Check if path is a file or foleder
```powershell
$path = "C:\Users\Tia\Desktop\code\it\powershell-script\test\file"

if (Test-Path -Path $path -PathType Leaf) {
    Write-Host "The path '$path' points to a file."
}
elseif (Test-Path -Path $path -PathType Container) {
    Write-Host "The path '$path' points to a folder."
}
else {
    Write-Host "The path '$path' does not exist."
}
```

## and condition
```powershell
$path1 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\manager"
$path2 = "C:\Users\Tia\Desktop\code\it\powershell-script\test\engineering"

$parent1 = Split-Path -Path $path1 -Parent
$parent2 = Split-Path -Path $path2 -Parent

$folder1 = Split-Path -Path $path1 -Leaf
$folder2 = Split-Path -Path $path2 -Leaf

Write-Host "The folder1: $parent1"
Write-Host "The folder2: $parent2"

Write-Host "The folder1: $folder1"
Write-Host "The folder2: $folder2"


if ((Test-Path -Path $path1 -PathType Container) -or (Test-Path -Path $path1 -PathType Leaf)) {
    Write-Host "The folder $folder1 exist"
    Write-Host "Removing $folder1 ------------------ please wait"
    Start-Sleep -Seconds 5
    Remove-Item -Path $path1 -Force -Recurse 
    Write-Host "The folder $folder1 was remove successfully"
}
else {
    Write-Host "The folder $folder1 does not exist"
}

if ((Test-Path -Path $path2 -PathType Container) -or (Test-Path -Path $path2 -PathType Leaf)) {
    Write-Host "The folder $folder2 exist"
    Write-Host "Removing $folder2 ------------------ please wait"
    Start-Sleep -Seconds 5
    Remove-Item -Path $path2 -Force -Recurse 
    Write-Host "The folder $folder2 was remove successfully"
}
else {
    Write-Host "The folder $folder2 does not exist"
}
```

## and, or condition
```powershell
$condition1 = $true
$condition2 = $false

if ($condition1 -or $condition2) {
    # Code to execute if either condition is true
    Write-Host "At least one condition is true"
} else {
    # Code to execute if both conditions are false
    Write-Host "Both conditions are false"
}
```

```powershell
$condition1 = $true
$condition2 = $false

if ($condition1 -and $condition2) {
    # Code to execute if both conditions are true
    Write-Host "Both conditions are true"
} else {
    # Code to execute if either condition is false
    Write-Host "At least one condition is false"
}
```

## Rename file and folder
```powershell
$folderPath = "C:\Users\Tia\Desktop\code\it\powershell-script\test\folder"
$filePath = "C:\Users\Tia\Desktop\code\it\powershell-script\test\file.txt"
$newFolderName = "new_folder"
$newFileName = "new_file.txt"

Rename-Item -Path $folderPath -NewName $newFolderName
Rename-Item -Path $filePath -NewName $newFileName
```

## Rename file and folder
```powershell
$folderPath = "C:\Users\Tia\Desktop\code\it\powershell-script\test\folder"
$filePath = "C:\Users\Tia\Desktop\code\it\powershell-script\test\file.txt"
$newFolderName = "new_folder"
$newFileName = "new_file.txt"


$folderName = Split-Path -Path $folderPath -Leaf
$fileName = Split-Path -Path $filePath -Leaf

Write-Host "The folderName: $folderName"
Write-Host "The fileName: $fileName"


if (Test-Path -Path $folderPath -PathType Container) {
    Write-Host "The folder $folderName exist"
    Write-Host "Reanaming $folderName ------------------ please wait"
    Start-Sleep -Seconds 5
    Rename-Item -Path $folderPath -NewName $newFolderName
    Write-Host "The folder $folderName was rename successfully"
}
else {
    Write-Host "The folder $folderName does not exist"
}

if (Test-Path -Path $filePath -PathType Leaf) {
    Write-Host "The file $fileName exist"
    Write-Host "Reanaming $fileName ------------------ please wait"
    Start-Sleep -Seconds 5
    Rename-Item -Path $filePath -NewName $newFileName
    Write-Host "The file $fileName was rename successfully"
}
else {
    Write-Host "The file $fileName does not exist"
}
```