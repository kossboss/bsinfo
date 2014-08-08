## bsinfo - BTRFS SNAPSHOT INFORMATION

Here is an attempt to use the method on this site http://dustymabe.com/2013/09/22/btrfs-how-big-are-my-snapshots/ to calculate the size of btrfs snapshots

Authors attempt only shows IDs, so in this version of output the snapshot paths are included. There are 2 formats of the scripts (should of just added an argument option isntead of having 2 different script, but whocares... maybe ill change it later)

**bsinfoI**: shows the btrfs snapshot sizes sorted by their btrfs ID

**bsinfoP**: shows the btrfs snapshot sizes sorted by their btrfs Path

This next part is in the comments of both bsinfoI and bsinfoP, however its important to include here as well

### more info:
The snapshot path information is grabbed from the output of "**btrfs subvolume list -p --sort=path /data**"
The snapshot size information is grabbed from the output of "**btrfs qgroup show /data**"
For this to work you might need to have btrfs quota globally enabled on your btrfs volume.
To enable btrfs quotas just type:
$ btrfs quota enable /data
where /data is your volumename

### HOW TO USE

download bsinfoI and bsinfoP
make them executable:

    chmod +x bsinfo*
    ./bsinfoI /data
    ./bsinfoP /data

where /data is your volume name

**NOTE**: read the comments to see any disclaimers etc...
