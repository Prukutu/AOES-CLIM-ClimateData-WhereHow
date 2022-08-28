---
title: "Where to get Climate Datasets"
teaching: 15
exercises: 5
questions:
- "Where do I find Climate Datasets?"
objectives:
- "Learning to find climate datasets on the web"
- "How and where to download a dataset from the web"
- "How to be a good citizen of `/homes`"
keypoints:
- "Don't download big datasets to your `/homes` directory!"
---

**Launch a Hopper Desktop session from your [ORC Dashboard](https://ondemand.orc.gmu.edu/pun/sys/dashboard/).**
We will use it for today's lesson.

### Where can I find Climate Datasets?

Many climate datasets are still available on the COLA servers, 
and will be migrated to Hopper in the comming months.
But how do I find this data? Where would I look to find a dataset that is not on the COLA servers?  
As I go forward in my research, how do I find datasets I might want to use?

1.  [COLA Datasets Catalog](https://kpegion.github.io/COLA-DATASETS-CATALOG/)  
We are in the process of cataloging all the dataests on the COLA servers.
This is a good place to start if you want to know what data are available locally.

2. [NOAA/Physical Sciences Lab](https://psl.noaa.gov/data/gridded/)
Many climate datasets are here with lots of information and searching capabilities.

3. [IRI/LDEO Climate Data Library](https://iridl.ldeo.columbia.edu/index.html?Set-Language=en)
This is another great resource for finding Climate Datasets.

4. [NCAR Climate Data Guide](https://climatedataguide.ucar.edu/)
Great resource for getting expert advice on NCAR's extensive Climate Data holdings, and which datasets you should use for your specific application.

5. [NASA Earth Data](https://www.earthdata.nasa.gov)
NASA has a large distributed archive of Climate Data, mainly from satellites, that is publicly available for download.


### Where should I put Climate Datasets?

There are two main ways to access and use climate datasets that are available on the web.

1. You can download a copy of the dataset to your local computer system, and analyze it there.

2. You can access, subset, and (depending on the data server) even analyze the data remotely, having only the result on your local computer system.

Since some climate datasets can be very large, and you may need to use many different ones, 
option #1 may require a sizeable amount of disk space to store the data. 
However, once you have a copy of the dataset locally, _you own it_ and you can easily use it over and over.

Option #2 will save space on your computer system, but may also slow down calculations, depending on Internet speed and the load on the remote data servers. It requires reaccessing the data remotely every time you make a change to your calculation.

Thus, there is a decision to be made depending on your situation - one or the other option will be the better choice.

> ## Being a wise computer citizen
>
> If you choose to download data sets to Hopper, recall that your home directory is limited to 50 GB. 
> If you fill up your home disk by downloading too many large datasets there, you may be locked out of the system until you clear space.
> 
> Aside from your home directory, there are three other categories of disks which may be a better choice, even for smaller data files:
> 
> 1. `/scratch` - for short-term storage of data. There is a nominal 90-day limit for file storage here, and old files are automatically deleted monthly. 
> 
> 2. `/tmp` - for temporary storage. This disk is mainly used by programs that are running on the cluster that need to temporarily store data on disk as part of their processes. This includes applications like your JupyterLab sessions. If you manually make directories or store files under `/tmp`, they will remain as long as your session is active, but will disappear as soon as it is not (when your Dashboard session times out, or if you log in via `ssh` in a terminal session, once your session is closed).  
> 
> 3. `/project` - for long-term storage of data. Only faculty and research staff can own `project` directories, which are 1 TB is size. They are associated with a **group** that includes only users specified by the owner. You should ask your advisor if they have a `project` disk on Hopper that you can share.
> 
> Soon there will be a fourth option. COLA will be moving 1PB of its data holdings to a new disk on Hopper, in late 2022 or early 2023. If you use those data, you will not need to make your own copies on the disk systems listed above. 
{: .callout}


### Downloading Climate Datasets with `wget`

The most common, and often the easiest, way to download data sets from the web is to use the command `wget` from a terminal session. 

From a terminal window logged in your Hopper desktop, change to the `/scratch` directory. 
If you already have your own subdirectory there, go to that.  If you do not, make one:

~~~
$ cd /scratch
$ mkdir <your_username>
$ cd <your_username>
~~~
{: .language-bash}

At one of the data repository websites listed above, let's find a dataset to download.  
In a browser, go to:
<a href="https://psl.noaa.gov/data/gridded/">https://psl.noaa.gov/data/gridded/</a> and scroll down to the entry:
<a href="https://psl.noaa.gov/data/gridded/data.noaa.ersst.v5.html">NOAA Extended Reconstructed SST V5</a>.
There you will find a web page with a nice description of the dataset.

In the section of the page called "Download/Plot Data", in the "download file" column you will see two datasets
for "Sea Surface Temperature" listed. 
Click on the _download_ icon for the "Long Term Mean" statistics.

On the new page, you will see a kind of directory listing with several files.
<u>Don't click</u>, but *right-click* on "sst.mon.ltm.1991-2020.nc" and choose "copy link address" to put the URL on your clipboard.
Then paste the link into your terminal after typing `wget`:

~~~
$ wget https://downloads.psl.noaa.gov/Datasets/noaa.ersst.v5/sst.mon.ltm.1991-2020.nc
~~~
{: .language-bash}

You will get some text on your screen like the following, that reports on the `wget` process:

~~~
[pdirmeye@hop043 pdirmeye]$ wget https://downloads.psl.noaa.gov/Datasets/noaa.ersst.v5/sst.mon.ltm.1991-2020.nc
--2022-08-28 14:09:08--  https://downloads.psl.noaa.gov/Datasets/noaa.ersst.v5/sst.mon.ltm.1991-2020.nc
Resolving downloads.psl.noaa.gov (downloads.psl.noaa.gov)... 140.172.38.86
Connecting to downloads.psl.noaa.gov (downloads.psl.noaa.gov)|140.172.38.86|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1160004 (1.1M) [application/x-netcdf]
Saving to: 'sst.mon.ltm.1991-2020.nc'

sst.mon.ltm.1991-2020.nc 100%[==================================>]   1.11M  4.72MB/s    in 0.2s    

2022-08-28 14:09:09 (4.72 MB/s) - 'sst.mon.ltm.1991-2020.nc' saved [1160004/1160004]
~~~
{: .output}

Note that the URL is not `http://` or `https://` but is `ftp://`. `ftp` stands for "file transfer protocol". 
It is an old, robust but insecure protocol for moving data that works well from web sites because it has an "anonymous" mode that does not require a user to log in to retrieve files. 
There is a secure version called `sftp` that uses `ssh` and requires passwords. 
`sftp` or `scp` (the secure copy command) are preferred over `ftp` for moving files between private sources (e.g. your Hopper account and an account you might have at a supercomuting center).

> ## There is a Broswer on Hopper
>
> Note: You have a browser available on your Hopper Desktop.
> There is a button at the bottom that will launch a Linux build of Firefox.
> You can use the _download_ capabilities of this browser to download files directly to your
> Hopper account. This could be a good option if you only have one or a few files to download 
> (that do not require a lot of clicking on links). 
> 
> However, GUI apps like browsers do not run very smoothly on HPC systems - they are not designed for that.
> So for larger or more complex downloads where you would benerfit by using wildcards or recursion, 
> It is probably better to use `wget` from the command line of a terminal window.
{: .callout}


{% include links.md %}

