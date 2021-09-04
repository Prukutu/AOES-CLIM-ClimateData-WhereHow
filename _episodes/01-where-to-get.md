---
title: "Where to get Climate Datasets"
teaching: 0
exercises: 0
questions:
- "Where do I find Climate Datasets?"
objectives:
- ""
keypoints:
- ""
---

### Where can I find Climate Datasets?

Many climate datasets are available on the COLA servers, but how do I find this data? Where would I look to find a dataset that is not on the COLA servers?  As I go forward in my research, how do I find datasets I might want to use?

1.  [COLA Datasets Catalog](https://kpegion.github.io/COLA-DATASETS-CATALOG/)  We are in the process of cataloging all the dataests on the COLA servers.
Not everything is there yet, but this is a good place to start if you want to know what data are available locally.

2. [NOAA/Physical Sciences Lab](https://psl.noaa.gov/data/gridded/)
Many climate datasets are here with lots of information and searching capabilities.  This is my go-to for finding climate datasets.

3. [IRI/LDEO Climate Data Library](https://iridl.ldeo.columbia.edu/index.html?Set-Language=en)
This is another great resource for finding Climate Datasets

4. [NCAR Climate Data Guide](https://climatedataguide.ucar.edu/)
Great resource for getting expert advice on which datasets you should use for your specific application


### Where shoild I put Climate Datasets?

There are two main ways to access and use climate datasets that are available on the web.

1. You can download a copy of the dataset to your local computer system, and analyze it there.

2. You can access, subset, and (depending on the data server) even analyze the data remotely, having only the result on your local computer system.

Since some climate datasets can be very large, and you may need to use many different ones, 
option #1 may require a sizeable amount of disk space to store the data. 
However, once you have a copy of the dataset locally, _you own it_ and you can easily use it over and over.

Option #2 will save space on your computer system, but may also slow down calculations, depending on Internet speed and the load on the remote data servers. It requires reaccessing the data remotely every time you make a change to your calculation.

Thus, there is a decision to be made depending on your situation - one or the other option will be the better choice.

> ## Being a good COLA computer citizen
>
> If you choose to download data sets to the COLA servers, **do not store them in your home directory!!**
> The `/homes` disk is a limited, shared and <u>critical</u> resource among all users. 
> If you fill up the `/homes` disk by downloading too many large datasets there, no one will be able to use system!
> 
> There are three categories of disks, denoted by three different top-level directories, where large datasets should be stored:
> 
> 1. `/scratch` - for temporary or non-critial data. This disk is not backed up, and old files may be scrubbed (deleted) if the disk becomes full.
> 
> 2. `/project` - for most working datasets. Each research project at COLA may have one or more project disks. 
> These disks are periodically backed up to tape, so they can be restored if there is a hardware failure or other problem.
> Check with your advisor for access to project disks relevant to your use. 
> 
> 3. `/shared` - for long-term, non-volitile datasets. These disks are where "final versions" of datasets are kept. 
> These may be datasets downloaded from sources like those above, that are deemed essential enough to have local copies, 
> or datasets produced by COLA scientists. Only new files get backed up, and it is assumed they will be rarely if ever changed once placed here.
> 
{: .callout}


### Downloading Climate Datasets with `wget`

The most common way to download data sets from the web is to use the unix command `wget`. 

From a terminal window logged in to one of the COLA servers, change to the `/scratch` directory. 
If you already have your own subdirectory there, go to that.  If you do not, make one:

~~~
$ cd /scratch
$ mkdir <your_username>
$ cd <your_username>
~~~
{: .language-bash}

At one of the data repository websites listed above, let's find a dataset to download.  In a browser, go to:
<a href="https://psl.noaa.gov/data/gridded/">https://psl.noaa.gov/data/gridded/</a> and scroll down to the entry:
<a href="https://psl.noaa.gov/data/gridded/data.noaa.ersst.v5.html">NOAA Extended Reconstructed SST V5</a>.
There you will find a web page with a nice description of the dataset.

In the section called "Download/Plot Data", in the "download file" column you will see two files listed. 
<u>Don't click</u>, but *right-click* on "sst.mon.ltm.1981-2010.nc" and choose "copy link address" to put the URL on your clipboard.
Then paste the link into your terminal after typing `wget`:

~~~
$ wget ftp://ftp.cdc.noaa.gov/Datasets/noaa.ersst.v5/sst.mon.ltm.1981-2010.nc
~~~
{: .language-bash}

You will get some text on your screen like the follwing, that reports on the `wget` process:

~~~
--2021-09-04 14:47:31--  ftp://ftp.cdc.noaa.gov/Datasets/noaa.ersst.v5/sst.mon.ltm.1981-2010.nc
           => ‘sst.mon.ltm.1981-2010.nc’
Resolving ftp.cdc.noaa.gov (ftp.cdc.noaa.gov)... 140.172.38.117
Connecting to ftp.cdc.noaa.gov (ftp.cdc.noaa.gov)|140.172.38.117|:21... connected.
Logging in as anonymous ... Logged in!
==> SYST ... done.    ==> PWD ... done.
==> TYPE I ... done.  ==> CWD (1) /Datasets/noaa.ersst.v5 ... done.
==> SIZE sst.mon.ltm.1981-2010.nc ... 1159964
==> PASV ... done.    ==> RETR sst.mon.ltm.1981-2010.nc ... done.
Length: 1159964 (1.1M) (unauthoritative)

100%[===================================================================================>] 1,159,964   --.-K/s   in 0.1s    

2021-09-04 14:47:37 (10.8 MB/s) - ‘sst.mon.ltm.1981-2010.nc’ saved [1159964]
~~~
{: .language-bash}

Note that the URL is not `http://` or `https://` but is `ftp://`. `ftp` stands for "file transfer protocol". 
It is an old, robust but insecure protocol for moving data that works well from web sites because it has an "anonymous" mode that does not require a user to log in to retrieve files. 
There is a secure version called `sftp` that uses `ssh` and requires passwords. 
`sftp` is the preferred method for moving files between private sources (e.g. your COLA account and an account you might have at a supercomuting center).

{% include links.md %}

