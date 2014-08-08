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
To enable btrfs quotas just type this:
$ btrfs quota enable /data
where /data is your volumename

### HOW TO USE

download bsinfoI and bsinfoP
make them executable:

    wget https://raw.githubusercontent.com/kossboss/bsinfo/master/bsinfoI
    wget https://raw.githubusercontent.com/kossboss/bsinfo/master/bsinfoP
    chmod +x bsinfoI
    chmod +x bsinfoP

if get errors on none-trust (because its github) use this:

    wget --no-check-certificate https://raw.githubusercontent.com/kossboss/bsinfo/master/bsinfoI
    wget  --no-check-certificate https://raw.githubusercontent.com/kossboss/bsinfo/master/bsinfoP
    chmod +x bsinfoI
    chmod +x bsinfoP
    
example of use:

    ./bsinfoI /data
    ./bsinfoP /data

where /data is your volume name

**NOTE**: read the comments to see any disclaimers etc...

### Example output:

    # ./bsinfoI /Sally
    id        ref(MB)         excl(MB)        path
    ----      ------          -------         -----
    0/5       0.01            0.01            ...n/a...
    0/259     434.68          434.68          /Sally/.apps
    0/260     0.03            0.03            /Sally/home
    0/263     0.04            0.04            /Sally/._share
    0/10283   584492.50       15153.64        /Sally/All
    0/10308   322326.04       322326.04       /Sally/Customer
    0/10309   3956.95         0.01            /Sally/readydrop
    0/10360   0.00            0.00            /Sally/home/kostia
    0/10409   748933.71       0.16                /Sally/._share/All/.snapshot/m_CoursesPreDelete
    0/10410   613369.78       0.07            /Sally/._share/All/.snapshot/m_CoursesComplete
    0/10411   0.00            0.00            /Sally/.purge
    0/10418   562657.16       207539.59       /Sally/._share/All/.snapshot/c_1404975613
    0/10487   51200.03        51200.03        /Sally/prox1
    0/10492   657.93          657.93          /Sally/prox1nfs
    0/10493   579222.36       9883.51         /Sally/._share/All/.snapshot/c_1407394835
    0/10495   0.00            0.00            /Sally/All/.snapshots
    0/10496   748934.45       6139.26         /Sally/All/.snapshots/1/snapshot
    0/10497   0.00            0.00            /Sally/readydrop/.snapshots
    0/10498   3956.95         0.01            /Sally/readydrop/.snapshots/1/snapshot
    0/10499   0.00            0.00            /Sally/.timemachine
    0/10500   0.00            0.00            ...n/a...

    # ./bsinfoP /Sally
    id        ref(MB)         excl(MB)        path
    ----      -------         --------        -----
    0/263     0.04            0.04            /Sally/._share
    0/10418   562657.16       207539.59       /Sally/._share/All/.snapshot/c_1404975613
    0/10493   579222.36       9883.51         /Sally/._share/All/.snapshot/c_1407394835
    0/10410   613369.78       0.07            /Sally/._share/All/.snapshot/m_CoursesComplete
    0/10409   748933.71       0.16            /Sally/._share/All/.snapshot/m_CoursesPreDelete
    0/259     434.68          434.68          /Sally/.apps
    0/10411   0.00            0.00            /Sally/.purge
    0/10499   0.00            0.00            /Sally/.timemachine
    0/10283   584492.50       15153.64        /Sally/All
    0/10495   0.00            0.00            /Sally/All/.snapshots
    0/10496   748934.45       6139.26         /Sally/All/.snapshots/1/snapshot
    0/10308   322326.04       322326.04       /Sally/Customer
    0/260     0.03            0.03            /Sally/home
    0/10360   0.00            0.00            /Sally/home/kostia
    0/10487   51200.03        51200.03        /Sally/prox1
    0/10492   657.93          657.93          /Sally/prox1nfs
    0/10309   3956.95         0.01            /Sally/readydrop
    0/10497   0.00            0.00            /Sally/readydrop/.snapshots
    0/10498   3956.95         0.01            /Sally/readydrop/.snapshots/1/snapshot

