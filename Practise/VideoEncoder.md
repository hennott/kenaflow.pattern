# The power of PowerShell in combination with kenaflow and Handbrake


## The working example script
This is a simple script for a List-Workflow. You need HandbrakeCLI installed on the computer where you rund this workflow.

```
param($wf, $web, $item, $config, $eventData)

if($wf-eq$null){import-module "D:\KenaFlow\Engine\kenaflow.runtime.dll";Invoke-Kenaflow;exit}

# Define where the source video is stored
$Source = "/Media_UploadFolder/"+$item['FileLeafRef']
# Define where the compressed video should be stored !! Attention this should be a diffent library
$SourceBackend = "/Media_Backend/"
# Define temporary used path on the local system
$Target = "D:\kenaflow\workflows\videoencoder\_tmp\"+$item.id+"\"
$TargetLog = $Target+"log.txt"
$TargetFile = $Target+$item['FileLeafRef']
$TargetFile_LQ = $Target+$item['FileLeafRef']+".min.mp4"

# Creat a path on the local machine to temporary store the videofile for encoding
New-Item -ItemType directory -Path $Target
# Download the video
Get-PnPFile -AsFile -Url $Source -Path $Target

# Use Handbrake to encode the video
Start-Process 'C:\Program Files\HandBrake\HandBrakeCLI.exe' -argumentlist @("-i",$TargetFile,"-o",$TargetFile_LQ) -Wait -RedirectStandardError $TargetLog

# Upload the encoded video
Add-PnPFile -Path $TargetFile_LQ -Folder $SourceBackend
# And finally delete the temporary folder
Remove-Item -Path $Target -Recurse -Force -Confirm:$false
```

You can use this example to build your own video encoder. It can make sense to encode the video multiple time for different resolutions .. so feel free to extend this example.
