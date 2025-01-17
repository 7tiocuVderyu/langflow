# How to Install and Run z/OS 1.13 ADCD on Hercules Emulator
 
z/OS is an operating system for IBM mainframes that supports a variety of applications and workloads. ADCD stands for Application Developer Controlled Distribution, which is a collection of z/OS software products that can be used for development and testing purposes. Hercules is an open source software that emulates IBM mainframe hardware and allows running z/OS on a PC.
 
In this article, we will show you how to install and run z/OS 1.13 ADCD on Hercules emulator on Ubuntu Linux 18.04.3 LTS. This is based on the instructions from GuangXingLiu[^2^], with some modifications and updates.
 
**DOWNLOAD ===== [https://tweeat.com/2uE8oD](https://tweeat.com/2uE8oD)**


 
## Prerequisites
 
Before you start, you will need the following:
 
- A PC with at least 12 GB of RAM and 100 GB of free disk space.
- Ubuntu Linux 18.04.3 LTS installed on your PC.
- Hercules 1.13 emulator installed on your PC. You can download it from [here](https://github.com/hercules-390/hyperion/releases).
- z/OS 1.13 ADCD CCKD files downloaded from [here](https://archive.org/details/zOS.113.f.2013.10). These are compressed disk images that contain the z/OS system and software products. You will need to unzip them before using them.
- A license key file for z/OS 1.13 ADCD. You can obtain it from [here](https://www.ibm.com/docs/en/developer-for-zos/14.0?topic=SSQ2R2_14.0.0/com.ibm.zsys.rdt.guide.activ.doc/topics/license_keys_and_ADCD.html).

## Steps

1. Create a folder for ADCD system. Open a terminal and type the following commands:

        sudo mkdir /home/ADCD
        sudo mkdir /home/ADCD/zos113
        sudo chmod 777 -R /home/ADCD

2. Copy the z/OS 1.13 ADCD CCKD files to the /home/ADCD/zos113 folder. You can use the ftp command or any other method to transfer the files from your download location to your PC.
3. Create a backup copy of the CCKD files in case they get corrupted. Type the following command:

        sudo cp -R /home/ADCD/zos113 /home/ADCD/zos113bk

4. Create a configuration file for Hercules emulator in the /home/ADCD/zos113 folder. Type the following command:

        sudo vim /home/ADCD/zos113/zos113.cnf

5. Copy and paste the following content into the configuration file and save it:

        # Hercules Emulator Control file...
        # Description: z/OS 1.13 Created by www.guangxing.name
        MaxShutdownSecs: 15
        
        # System parameters
        ARCHMODE z/Arch
        ALRF ENABLE
        CNSLPORT 3270
        CONKPALV (3,1,10)
        CPUMODEL 3090
        CPUSERIAL 012345
        DIAG8CMD ENABLE
        ECPSVM NO
        LOADPARM 0A821WM1
        LPARNAME HERCULES
        MAINSIZE 12000
        MOUNTED_TAPE_REINIT DISALLOW
        NUMCPU 2
        OSTAILOR Z/OS
        PANRATE 80
        PGMPRDOS LICENSED
        SHCMDOPT NODIAG8
        SYSEPOCH 1900
        TIMERINT 50
        TZOFFSET +0000
        YROFFSET 0
        
        HERCPRIO 0
        TODPRIO -20
        DEVPRIO 8
        CPUPRIO 0
        
        PANTITLE "z/OS 1.13 IPL A80"
        
        # Display Terminals
        0700-0709   3270
        
        # DASD Devices
        0A80 3390 /home/ADCD/zos113/ZDRES1.CCKD sf=/home/ADCD/zos113/ZDRES1_Shadow.CCKD
        0A81 3390 /home/ADCD/zos113/ZDRES2.CCKD sf=/home/ADCD/zos113/ZDRES2_Shadow.CCKD
        0A82 3390 /home/ADCD/zos113/ZDSYS1.CCKD sf=/home/ADCD/zos113/ZDSYS1_Shadow.CCKD
        0A83 3390 /home/ADCD/zos113/ZDUSS1.CCKD sf=/home/ADCD/zos113/ZDUSS1_Shadow.CCKD
        0A84 3390 /home/ADCD/zos113/ZDPRD1.CCKD sf=/home/ADCD/zos113/ZDPRD1_Shadow.CCKD
        0A85 3390 /home/ADCD/zos113/ZDPRD2.CCKD sf=/home/ADCD/zos113/ZDPRD2_Shadow.CCKD
        0A86 3390 /home/ADCD/zos113/ZDPRD3.CCKD sf=/home/ADCD/zos113/ZDPRD3_Shadow.CCKD
        0A87 3390 /home/ADCD/zos113/ZDDIS1.CCKD sf=/home/ADCD/zos113/ZDDIS1_Shadow.CCKD
        0A88 3390 /home/ADCD/zos113/ZDDIS2.CCKD sf=/home/ADCD/zos113/ZDDIS2_Shadow.CCKD
        0A89 3390 /home/ADCD/zos113/ZDDIS3.CCKD sf=/home/ADCD/zos113/ZDDIS3_Shadow.CCKD
        0A8A 3390 /home/ADCD/zos113/ZDDIS4.CCKD sf=/home/ADCD/zos113/ZDDIS4_Shadow.CCKD
        0A8B 3390 /home/ADCD/zos113/ZDDIS5.CCKD sf=/home/ADCD/zos113/ZDDIS5_Shadow.CCKD
        0A8C 3390 /home/ADCD/zos113/ZDDIS6.CCKD sf=/home/ADCD/zos113/ZDDIS6_Shadow.CCKD
        0A8D 3390 /home/ADCD/zos113/ZDPAGA.CCKD sf=/home/ADCD/zos113/ZDPAGA_Shadow.CCKD
        0A8E 3390 /home/ADCD/zos113/ZDPAGB.CCKD sf=/home/ADCD/zos113/ZDPAGB_Shadow.CCKD
        0A8F 3390 /home/ADCD/zos113/ZDPAGC.CCKD sf=/home/ADCD/zos113/ZDPAGC_Shadow.CCKD
        0A90 3390 /home/ADCD/zos113/ZDPAGD.CCKD sf=/home/ADCD/zos113/ZDPAGD_Shadow.CCKD
        0A91 3390 /home/ADCD/zos113/ZDPAGE.CCKD sf=/home/ADCD/zos113/ZDPAGE_Shadow.CCKD
        0A92 3390 /home/ADCD/zos113/ZDPAGF.CCKD sf=/home/ADCD/zos113/ZDPAGF_Shadow.CCKD
        0A93 3390 /home/ADCD/zos113/SARES1.CCKD sf=/home/ADCD/zos113/SARES1_Shadow.CCKD
        0A94 3390 /home/ADCD/zos113/VDDA1A.CCKD sf=/home/ADCD/zos113/VDDA1A_Shadow.CCKD
        0A95 3390 /home/ADCD/zos113/VDDA1B.CCKD sf=/home/ADCD/zos113/VDDA1B_Shadow.CCKD
        0A96 3390 /home/ADCD/zos113/VDUTAA.CCKD sf=/home/ADCD/zos113/VDUTAA_Shadow.CCKD
        0A97 3390 /home/ADCD/zos113/VDUTAB
        z os adcd 1.13 122 download, 
        z os adcd 1.13 122 installation, 
        z os adcd 1.13 122 license key, 
        z os adcd 1.13 122 gzip format, 
        z os adcd 1.13 122 zpdt, 
        z os adcd 1.13 122 linux, 
        z os adcd 1.13 122 system requirements, 
        z os adcd 1.13 122 application development, 
        z os adcd 1.13 122 rational test environment, 
        z os adcd 1.13 122 ibm dallas, 
        z os adcd 1.13 122 dvd packet, 
        z os adcd 1.13 122 electronic download, 
        z os adcd 1.13 122 subscription fee, 
        z os adcd 1.13 122 disclaimer, 
        z os adcd 1.13 122 announcements, 
        z os adcd 1.13 122 sunset date, 
        z os adcd 1.13 122 contents, 
        z os adcd 1.13 122 products, 
        z os adcd 1.13 122 problems and fixes, 
        z os adcd 1.13 122 maintenance service levels, 
        z os adcd 1.13 122 build structure, 
        z os adcd 1.13 122 migration guidelines, 
        z os adcd 1.13 122 loadparms options, 
        z os adcd 1.13 122 console pf key settings, 
        z os adcd 1.13 122 userids, 
        z os adcd v2r4 july edition, 
        how to request the z os adcd v2r4 july edition, 
        how to install the z os adcd v2r4 july edition, 
        how to activate the license key for the z os adcd v2r4 july edition, 
        how to use the Z1091_ADCD_install command for the z os adcd v2r4 july edition, 
        how to run the z os adcd v2r4 july edition under zd&t enterprise edition, 
        how to access the web interface for the z os adcd v2r4 july edition, 
        how to configure the network settings for the z os adcd v2r4 july edition, 
        how to customize the system parameters for the z os adcd v2r4 july edition, 
        how to start and stop the system for the z os adcd v2r4 july edition, 
        how to log on and off the system for the z os adcd v2r4 july edition, 
        how to submit jobs and view output for the z os adcd v2r4 july edition, 
        how to use tso/e, ispf, and sdsf for the z os adcd v2r4 july edition, 
        how to use cics, db2, ims, mq, and websphere for the z os adcd v2r4 july edition, 
        how to use cobol, pl/i, assembler, java, and rexx for the z os adcd v2r4 july edition, 
        how to use rational developer for system z with the z os adcd v2r4 july edition, 
        how to use rational test automation server with the z os adcd v2r4 july edition, 
        how to use rational team concert with the z os adcd v2r4 july edition, 
        how to use rational integration tester with the z os adcd v2r4 july edition, 
        how to use rational performance tester with the z os adcd v2r4 july edition, 
        how to use rational quality manager with the z os adcdbv2r4julyedition 8cf37b1e13

        
