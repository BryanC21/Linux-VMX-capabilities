# CMPE283 Assignment 1

## Team Members
Bryan Caldera

## Questions
1. I worked on this alone. 
2. This project checks various MSRs in Intel processors to find vmx capability support. The program will run as a kernel module and tell the user if the control can be set or cleared. To complete this assignment I first started by using the cmpe283-1.c and Makefile provided for this assignment. My next step was finding all the MSR addresses for Entry / Exit / Procbased / Secondary Procbased / Tertiary Procbased / Pinbased controls. I did not include Tertiary Procbased capabilities in my test as my CPU did not support it, the check is in the code just commented out. After this I copied the bit positions and command pairs from the Intel SDM, and wrote them into my capability_info structs. Then, I added code to check all the MSRs. To test this code I created an Ubuntu Virtual Machine using VMWARE on my Intel based Mac with nested virtualization enabled. I then used the following steps to run this C file and check for vmx capabilities. 

# Steps
* Have a Linux VM or Local Linux Machine

* Copy the files from the repository to your linux machine
`git clone https://github.com/BryanC21/vmx_lab_cmpe283.git`

* Install linux headers
`sudo apt-get install linux-headers-$(uname -r)`

* Install gcc make
`sudo apt-get install build-essential`

* Compile files
`make`

* Install Module
`sudo insmod cmpe283-1.ko`

* Remove Module
`sudo rmmod cmpe283-1.ko`

* Print result
`sudo dmesg`

## Output From My Intel Mac

[ 1513.791583] CMPE 283 Assignment 1 Module Start
[ 1513.791641] 
               Pinbased Controls MSR: 0x3f0000003f
[ 1513.791644]   External Interrupt Exiting: Can set=Yes, Can clear=No
[ 1513.791645]   NMI Exiting: Can set=Yes, Can clear=No
[ 1513.791645]   Virtual NMIs: Can set=Yes, Can clear=No
[ 1513.791646]   Activate VMX Preemption Timer: Can set=No, Can clear=Yes
[ 1513.791647]   Process Posted Interrupts: Can set=No, Can clear=Yes
[ 1513.791655] 
               Procbased Controls MSR: 0xf5f9fffe9501e97a
[ 1513.791657]   Interrupt-window exiting: Can set=Yes, Can clear=Yes
[ 1513.791658]   Use TSC offsetting: Can set=Yes, Can clear=No
[ 1513.791659]   HLT exiting: Can set=Yes, Can clear=Yes
[ 1513.791659]   INVLPG exiting: Can set=Yes, Can clear=Yes
[ 1513.791660]   MWAIT exiting: Can set=Yes, Can clear=Yes
[ 1513.791661]   RDPMC exiting: Can set=Yes, Can clear=No
[ 1513.791662]   RDTSC exiting: Can set=Yes, Can clear=Yes
[ 1513.791663]   CR3-load exiting: Can set=Yes, Can clear=No
[ 1513.791663]   CR3-store exiting: Can set=Yes, Can clear=No
[ 1513.791664]   Activate tertiary controls: Can set=No, Can clear=Yes
[ 1513.791665]   CR8-load exiting: Can set=Yes, Can clear=Yes
[ 1513.791666]   CR8-store exiting: Can set=Yes, Can clear=Yes
[ 1513.791667]   Use TPR shadow : Can set=Yes, Can clear=Yes
[ 1513.791667]   NMI-window exiting: Can set=Yes, Can clear=Yes
[ 1513.791668]   MOV-DR exiting: Can set=Yes, Can clear=Yes
[ 1513.791669]   Unconditional I/O exiting: Can set=Yes, Can clear=No
[ 1513.791670]   Use I/O bitmaps: Can set=No, Can clear=Yes
[ 1513.791671]   Monitor trap flag: Can set=No, Can clear=Yes
[ 1513.791671]   Use MSR bitmaps: Can set=Yes, Can clear=No
[ 1513.791672]   MONITOR exiting: Can set=Yes, Can clear=Yes
[ 1513.791673]   PAUSE exiting: Can set=Yes, Can clear=Yes
[ 1513.791674]   Activate secondary controls: Can set=Yes, Can clear=No
[ 1513.791681] 
               VM-Exit Controls MSR: 0x3fefff00036dff
[ 1513.791683]   Save debug controls: Can set=Yes, Can clear=No
[ 1513.791683]   Host address-spac size: Can set=Yes, Can clear=Yes
[ 1513.791684]   Load IA32_PERF_GLOBAL_CTRL: Can set=No, Can clear=Yes
[ 1513.791685]   Acknowledge interrupt on exit: Can set=Yes, Can clear=Yes
[ 1513.791686]   Save IA32_PAT: Can set=Yes, Can clear=Yes
[ 1513.791686]   Load IA32_PAT: Can set=Yes, Can clear=Yes
[ 1513.791687]   Save IA32_EFER: Can set=Yes, Can clear=Yes
[ 1513.791688]   Load IA32_EFER: Can set=Yes, Can clear=Yes
[ 1513.791689]   Save VMX-preemption timer value: Can set=No, Can clear=Yes
[ 1513.791689]   Clear IA32_BNDCFGS: Can set=No, Can clear=Yes
[ 1513.791690]   Conceal VMX from PT: Can set=No, Can clear=Yes
[ 1513.791691]   Clear IA32_RTIT_CTL: Can set=No, Can clear=Yes
[ 1513.791692]   Clear IA32_LBR_CTL: Can set=No, Can clear=Yes
[ 1513.791711]   Load CET state: Can set=No, Can clear=Yes
[ 1513.791712]   Load PKRS: Can set=No, Can clear=Yes
[ 1513.791713]   Save IA32_PERF_GLOBAL_CTL: Can set=No, Can clear=Yes
[ 1513.791714]   Activate secondary controls: Can set=No, Can clear=Yes
[ 1513.791721] 
               VM-Entry Controls MSR: 0xd3ff000011ff
[ 1513.791724]   Load debug controls: Can set=Yes, Can clear=No
[ 1513.791724]   IA-32e mode guest: Can set=Yes, Can clear=Yes
[ 1513.791725]   Entry to SMM: Can set=No, Can clear=Yes
[ 1513.791726]   Deactivate dualmonitor treatment: Can set=No, Can clear=Yes
[ 1513.791727]   Load IA32_PERF_GLOBAL_CTRL: Can set=No, Can clear=Yes
[ 1513.791738]   Load IA32_PAT: Can set=Yes, Can clear=Yes
[ 1513.791738]   Load IA32_EFER: Can set=Yes, Can clear=Yes
[ 1513.791739]   Load IA32_BNDCFGS: Can set=No, Can clear=Yes
[ 1513.791740]   Conceal VMX from PT: Can set=No, Can clear=Yes
[ 1513.791740]   Load IA32_RTIT_CTL: Can set=No, Can clear=Yes
[ 1513.791741]   Load CET state: Can set=No, Can clear=Yes
[ 1513.791742]   Load guest IA32_LBR_CTL: Can set=No, Can clear=Yes
[ 1513.791743]   Load PKRS: Can set=No, Can clear=Yes
[ 1513.791751] 
               Secondary Procbased Controls MSR: 0x111cfe00000000
[ 1513.791752]   Virtualize APIC accesses: Can set=No, Can clear=Yes
[ 1513.791753]   Enable EPT: Can set=Yes, Can clear=Yes
[ 1513.791754]   Descriptor-table exiting: Can set=Yes, Can clear=Yes
[ 1513.791755]   Enable RDTSCP: Can set=Yes, Can clear=Yes
[ 1513.791756]   Virtualize x2APIC mode: Can set=Yes, Can clear=Yes
[ 1513.791756]   Enable VPID: Can set=Yes, Can clear=Yes
[ 1513.791757]   WBINVD exiting: Can set=Yes, Can clear=Yes
[ 1513.791758]   Unrestricted guest: Can set=Yes, Can clear=Yes
[ 1513.791759]   APIC-register virtualization: Can set=No, Can clear=Yes
[ 1513.791760]   Virtual-interrupt delivery: Can set=No, Can clear=Yes
[ 1513.791760]   PAUSE-loop exiting: Can set=Yes, Can clear=Yes
[ 1513.791761]   RDRAND exiting: Can set=Yes, Can clear=Yes
[ 1513.791762]   Enable INVPCID: Can set=Yes, Can clear=Yes
[ 1513.791763]   Enable VM functions: Can set=No, Can clear=Yes
[ 1513.791763]   VMCS shadowing: Can set=No, Can clear=Yes
[ 1513.791764]   Enable ENCLS exiting: Can set=No, Can clear=Yes
[ 1513.791765]   RDSEED exiting: Can set=Yes, Can clear=Yes
[ 1513.791765]   Enable PML: Can set=No, Can clear=Yes
[ 1513.791766]   EPT-violation #VE: Can set=No, Can clear=Yes
[ 1513.791767]   Conceal VMX from PT: Can set=No, Can clear=Yes
[ 1513.791768]   Enable XSAVES/XRSTORS: Can set=Yes, Can clear=Yes
[ 1513.791769]   Mode-based execute control for EPT: Can set=No, Can clear=Yes
[ 1513.791770]   Sub-page write permissions for EPT: Can set=No, Can clear=Yes
[ 1513.791770]   Intel PT uses guest physical addresses: Can set=No, Can clear=Yes
[ 1513.791771]   Use TSC scaling: Can set=No, Can clear=Yes
[ 1513.791772]   Enable user wait and pause: Can set=No, Can clear=Yes
[ 1513.791773]   Enable PCONFIG: Can set=No, Can clear=Yes
[ 1513.791774]   Enable ENCLV exiting: Can set=No, Can clear=Yes
[ 1521.417231] CMPE 283 Assignment 1 Module Exits

