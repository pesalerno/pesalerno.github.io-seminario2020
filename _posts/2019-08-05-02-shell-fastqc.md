---
layout: default
order: 8
title:  "Getting Started in Shell"
date:   2019-08-05
time:   "08:30-09:30"
categories: main
instructor: "Becca"
materials: files/fakefile.txt
material-type: ""
lesson-type: Interactive
---


### Getting started in shell  
<br>

## The linux environment

### File systems
- your computer contains a nested hierarchy of directories
- **directory** is a *folder* on your computer which contains files
- keeping track of where you are in the file structure of your computer is an important component of computing
- highest level is the **root** (denoted: `/`)
- forward slashes divide levels in the nested hierarchy of directories, e.g. `/top_level_directory/second_level_directory`
- there are several high-level directories that users don't usually go into where program files are stored
	- /usr/bin
	- /usr/lib
- every file on your computer has an address; if you are going to do an operation on a file, you need its address
- **path**: the *address* to a directory or file on your computer. There are, generally, two types of paths:
	- **absolute/full path** represents the path of a given directory or file beginning at the root directory
    - **relative path** represents the path of a given directory/file relative to the working/current directory
- for example, say you have a file "my_favorite_file.txt" located in the directory `/Users/myname/Desktop/my_directory`.
	- the **full path** to this file  is `/Users/myname/Desktop/my_directory/my_favorite_file.txt`
    - the **relative path** to this file depends on where you are on the computer
	- if you are calling this file from Desktop, the relative path would be `my_directory/my_favorite_file.txt`
	- if you are in `/Users/myname/`, the relative path becomes `Desktop/my_directory/my_favorite_file.txt`
    
Remember - *Whenever you call the full path, you can reach the file from anywhere on your computer. Relative paths will change based on your current location.*

### Unix
- commands are small programs
	- type the name of a command and hit enter
	- Unix searches for the program's text file and executes it
- programs have preset arguments which change their behavior
	- these can be found in the program's manual
- programs interact with files that are in the directory that you are in
- we use a "shell" to interact with Unix: it exchanges information between user and program through *standard streams*
- **standard input**: input to programs
- **standard output**: information on screen, i.e. what the program outputs
- standard text editor for Unix is nano
	- type `nano` to access it
	- opens a text editor within the shell
	- saving, exiting, and other functions are controlled with ctrl + letter keys
	- we will be using primarily the Atom text editor instead of nano


### Here are some commands you will use all the time, we will review them as we proceed with the lesson

Command | Translation | Examples
--------|-------------|---------
`cd` | **c**hange **d**irectory | `cd /absolute/path/of/the/directory/` <br> Go to the home directory by typing simply  `cd` or `cd ~` <br> Go up (back) a directory by typing `cd ..`
`pwd` | **p**rint **w**orking **d**irectory | `pwd`
`mkdir` | **m**ake **dir**ectory | `mkdir newDirectory` creates newDirectory in your current directory <br> Make a directory one level up with `mkdir ../newDirectory`
`cp` | **c**o<b>p</b>y | `cp file.txt newfile.txt` (and file.txt will still exist!)
`mv` | **m**o<b>v</b>e | `mv file.txt newfile.txt` (but file.txt will *no longer* exist!)
`rm` | **r**e<b>m</b>ove | `rm file.txt` removes file.txt <br> `rm -r directoryname/` removes the directory and all files within
`ls` | **l**i<b>s</b>t | `ls *.txt` lists all .txt files in current directory <br> `ls -a` lists all files including hidden ones in the current directory <br> `ls -l` lists all files in current directory including file sizes and timestamps <br> `ls -lh` does the same but changes file size format to be **h**uman-readable <br> `ls ../` lists files in the directory above the current one
`man` | **man**ual | `man ls` opens the manual for command `ls` (use `q` to escape page)
`grep` | **g**lobal **r**egular <br> **e**xpression **p**arser |  `grep ">" seqs.fasta` pulls out all sequence names in a fasta file <br> `grep -c ">" seqs.fasta` counts the number of those sequences <br> 
`cat` | con<b>cat</b>enate | `cat seqs.fasta` prints the contents of seqs.fasta to the screen (ie stdout)
`head` | **head** | `head seqs.fasta` prints the first 10 lines of the file <br> `head -n 3 seqs.fasta` prints first 3 lines
`tail` | **tail** | `tail seqs.fasta` prints the last 10 lines of the file <br> `tail -n 3 seqs.fasta` prints last 3 lines
`wc` | **w**ord **c**ount | `wc filename.txt` shows the number of new lines, number of words, and number of characters <br> `wc -l filename.txt` shows only the number of new lines <br> `wc -c filename.txt` shows only the number of characters
`sort` | **sort** | `sort filename.txt` sorts file and prints output
`uniq` | **uniq**ue | `uniq -u filename.txt` shows only unique elements of a list <br> (must use sort command first to cluster repeats)

<br>
<br>

### Handy dandy shortcuts

Shortcut | Use|
----------|-----|
Ctrl + C | kills current process
Ctrl + L <br> (or `clear`) | clears screen
Ctrl + A | Go to the beginning of the line
Ctrl + E | Go to the end of the line
Ctrl + U | Clears the line before the cursor position
Ctrl + K | Clear the line after the cursor
`*` | wildcard character
tab | completes word
Up Arrow | call last command
`.` | current directory
`..` | one level up 
`~` | home
`>` | redirects stdout to a file, *overwriting* file if it already exists
`>>` | redirects stdout to a file, *appending* to the end of file if it already exists
pipe (<code>&#124;</code>) | redirects stdout to become stdin for next command


Keep in mind:
Good judgment comes from experience
experience comes from bad judgment
go make mistakes


### Download data for this lesson
```bash
cd # go to root of file system
mkdir workshop 
cd workshop
curl -L -O https://github.com/rdtarvin/IBS2019_Genomics-of-Biodiversity/blob/master/data/epiddrad_t200_R[1-2]_.fastq.gz?raw=true
# curl is a way to transfer files using a url from the command line
# -O option makes curl write to a file rather than stdout
# -L option forces curl to follow a redirect (determined by the web address)
# [1-2] downloads files that have a 1 or a 2 in that position
```

### Looking at your raw data in the linux environment

Your files will likely be gzipped and with the file extension **.fq.gz** or **fastq.gz**. The first thing you want to do is look at the beginning of your files while they are still gzipped.

```
ls # list all files in current directory
ls .. # list all files in one directory above
# rename files
mv epiddrad_t200_R1_.fastq.gz?raw=true epiddrad_t200_R1_.fastq.gz
mv epiddrad_t200_R2_.fastq.gz?raw=true epiddrad_t200_R2_.fastq.gz
```
Let's move these files into a new directory

```bash
mkdir epi
mv *.gz epi
ls
cd epi
ls -lht # -l = long format, -h = human readable, -t = order by time
```
Great! Now let's look at the files.

```bash
head epiddrad_t200_R1_.fastq.gz
```

Oops, what happened?! This gibberish is because of the format of the file, which is "gz" or "g-zipped". Let's unzip


```bash
gunzip *.gz
ls -lht
```
You can see that the size of the files expanded. Now try to peek:

```bash
head epiddrad_t200_R1_.fastq
```
This is the fastq format, which has four lines. 

```
@K00179:78:HJ2KFBBXX:5:1121:25844:7099 1:N:0:TGACCA+AGATCT
GCATGCATGCAGCTTCTTCCTTCACATGATCTTCCACACGGTGCTTAGCTTTTTATAAAGGTGACTTCACGCACCGCGTTCATTGCAGTCAGAAGTGGCTTCAAAGGGAAATGGAAATGAATGACTTTTACTTCTCCTTTTCTCTGGATC
+
AAFFFF7FF7AAJFFJJJJJJJJJJJJJFJJFFJJJF<AFF-FFJJ<JJFJFF-F--7AJJ<J<JFJJ-FFFJF-AFJFJAFJJJJJJJJFA7AFFFFFJ7JAJAJJJ<J<7FF7A-AAJJJ<FJ-77A7FFAA-AAAAFF7FJJF<AFJ

# sequencer name:run ID:flowcell ID:flowcell lane:tile number in flow cell:x-coordinate of cluster :y-coordinate pair member:filtered?:control data:index sequence
# DNA sequence
# separator, can also sometimes (not often) hold extra information about the read
# quality score for each base
```


Ok, now lets look at the full file with the `cat` program:

```bash
cat epiddrad_t200_R1_.fastq
```

Uh oh... let's quit before the computer crashes... it's too much to look at! `Ctrl+C`<br><br>
This is the essential computational problem with NGS data that is so hard to get over. You can't
open a file in its entirety! Here are some alternative ways to view parts of a file at a time.


	# print the first 10 lines of a file
	head epiddrad_t200_R1_.fastq

	# print the first 20 lines of a file
	head epiddrad_t200_R1_.fastq -20 # '-20' is an argument for the 'head' program

	# print lines 190-200 of a file
	head -200 epiddrad_t200_R1_.fastq | tail # 'pipes' the first 200 lines to a program called tail, which prints the last 10 lines

	# view the file interactively
	less epiddrad_t200_R1_.fastq # can scroll through file with cursor, page with spacebar; quit with 'q'
	# NOTE: here we can use less because the file is not in gzipped (remember that required the 'zless' command)

	# open up manual for less program
	man less # press q to quit

	# print only the first 10 lines and only the first 30 characters of each line
	head -200 epiddrad_t200_R1_.fastq | cut -c -30 

	# count the number of lines in the file
	wc -l epiddrad_t200_R1_.fastq # (this takes a moment because the file is large)

	# print lines with AAAAA in them
	grep 'AAAAA' epiddrad_t200_R1_.fastq # ctrl+c to exit

	# count lines with AAAAA in them
	grep -c 'AAAAA' epiddrad_t200_R1_.fastq

	# save lines with AAAAA in them as a separate file
	grep 'AAAAA' epiddrad_t200_R1_.fastq > AAAAA # no file extensions necessary!!

	# add lines with TTTTT to the AAAAA file: '>' writes or overwrites file; '>>' writes or appends to file
	grep 'TTTTT' epiddrad_t200_R1_.fastq >> AAAAA 

	# print lines with aaaaa in them
	grep 'aaaaa' epiddrad_t200_R1_.fastq
	# why doesn't this produce any output?

	# count number of uniq sequences in file with pattern 'AGAT'
	grep 'AGAT' epiddrad_t200_R1_.fastq | sort | uniq | wc -l

	# print only the second field of the sequence information line
	head epiddrad_t200_R1_.fastq | grep '@' | awk -F':' '{ print $2 }' 
	# awk is a very useful program for parsing files; here ':' is the delimiter, $2 is the column location




**Challenge**
<details> 
  <summary>How would you count the number of reads in your file? </summary>
   There are lots of answers for this one. One example: in the fastq format, the character '@' occurs once per sequence, so we can just count how many lines contain '@'.<br> 
   <code>gzcat epiddrad_t200_R1_.fastq.gz | grep -c '@'</code>
</details> 



# Time to start the assembly process!

![](https://github.com/rdtarvin/IBS2019_Genomics-of-Biodiversity/blob/master/images/basic-assembly-steps.png?raw=true)<br>

In this workflow, we will use [fastqc](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) to check read quality, 
[STACKS](http://catchenlab.life.illinois.edu/stacks/) for filtering and trimming, 
and then [iPyrad](http://ipyrad.readthedocs.io/index.html) for the rest of the assembly.<br><br>


Step 0. Use fastqc to check read quality.
---


	# fastqc is already installed, but if you wanted to download it, this is how: 
	# curl -L -O https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.5.zip
	# unzip fastqc_v0.11.5.zip

	# let's take a look at fastqc options
	/usr/local/bin/FastQC/fastqc -h
	/usr/local/bin/FastQC/fastqc *.fastq


When the program is finished, take a look at what files are in the directory using `ls`.
fastqc produces a nice .html file that can be viewed in any browser. <br>
Since we are trying to get comfortable with the command line, let's open the file directly.

	open epiddrad_t200_R1__fastqc.html 


Sequencing quality scores, "Q", run from 20 to 40. In the fastq file, these are seen as ASCII characters. 
The values are log-scaled: 20 = 1/100 errors; 30 = 1/1000 errors. Anything below 20 is garbage and anything between 20 and 30 should be reviewed.
There appear to be errors in the kmer content, but really these are just showing where the barcodes and restriction enzyme sites are. 
Let's take a look at what ddRAD reads look like:

![](https://github.com/rdtarvin/IBS2019_Genomics-of-Biodiversity/blob/master/images/ddRAD-read.png?raw=true)

Ok, we can see that overall our data are of high quality (high Q scores, no weird tile patterns, no adaptor contamination). Let's clean up our files and then move on to the assembly!!

```bash
mkdir fastqc
mv *__* fastqc 
gzip *.fastq
```



Step 1. Demultiplex by barcode in **STACKS**
---

Demultiplexing your sequencing pools is always the first step in any pipeline. In stacks, the files you need for demultiplexing are: 

- barcodes+sample names (tab-delimited .txt file)

- process_radtags code (shell program from stacks)

First, let's take a look at the Stacks Manual for [process_radtags](http://catchenlab.life.illinois.edu/stacks/comp/process_radtags.php) to see how to set up our barcodes file. 

So, let's build the barcodes file for demultiplexing, where the first column will be the unique adapter sequence using the second column in this [text file](https://raw.githubusercontent.com/rdtarvin/IBS2019_Genomics-of-Biodiversity/master/data/epi_barcodes.txt), the second column is the index primer sequence (in this case, AGATCT), and the third column is the individual sample names (first column in the referenced file). 

**There are MANY ways to build this file.... how do you want to do it?**

**NOTE**: whenever editing text files, first, NEVER use what you exported from excel or word directly… always check in a simple text editor (Text Wrangler, BBEdit, etc) and using “view invisible characters” to avoid unnecesary headaches of hidden characters or extra spaces/tabs, etc! Biggest waste of time in anything computing…


<details> 
  <summary>Side-note </summary>
   grep (Global regular expression print) is one of the most amazing things about text editors. <br>
   Try this on the epi_barcodes.txt file. Cmd+f, make sure 'grep' is checked, then search for
	<code>(.*)\t(.*)</code> and replace with <code>\2\tAGATCT\t\1</code>
</details> 



The general code we will use for process_radtags, running it from within the raw-data folder, is the following: 

	process_radtags -P -p . -b ./epi_barcodes_final.txt -o ./demultiplex -c -q -r -D --inline_index --renz_1 sphI --renz_2 mluCI -i gzfastq --disable_rad_check


**What do our demultiplexed files look like...?**


<br><br>

<a href="https://rdtarvin.github.io/RADseq_Quito_2017/"><button>Home</button></a>    <a href="https://rdtarvin.github.io/RADseq_Quito_2017/main/2017/08/02/afternoon-2bRAD-pyrad.html"><button>Next Lesson</button></a>


## Appendix

Pati will run the rest of the stacks pipeline on a different dataset. Here are the commands to finish this dataset and create data for the phylogenetics lesson later today.



Genotyping in stacks
----

In most cases, having a reference genome is a bad thing. However, STACKS is designed for non-model organisms, so in fact their [denovo_map](http://catchenlab.life.illinois.edu/stacks/comp/denovo_map.php) algorithms are superior and more self-contained than their [ref_map](http://catchenlab.life.illinois.edu/stacks/comp/ref_map.php) algorithms. 

In **ref_map.pl** you need to use [another alignment tool](https://github.com/lh3/bwa) prior to running stacks. So then, the pipeline workflow would have one extra step: 

	process_radtags
	GSNAP or bwa
	ref_map.pl

*"The ref_map.pl program takes as input aligned reads. It does not provide the assembly parameters that denovo_map.pl does and this is because the job of assembling the loci is being taken over by your aligner program (e.g. BWA or GSnap). You must take care that you have good alignmnets -- discarding reads with multiple alignments, making sure that you do not allow too many gaps in your sequences (otherwise loci with repeat elements can easily be collapsed during alignments), and take care not to allow soft-masking in the alignments. This occurs when an aligner can not make a full alignment and instead soft-masks the portion of the read that could not be aligned (pretending that this part of the read does not exist). **These factors, if not cared for, can cause spurious SNP calls and problems in the downstream analysis."***

A recent paper that came out, [Lost in Parameter Space: a roadmap for STACKS](http://onlinelibrary.wiley.com/doi/10.1111/2041-210X.12775/full), shows how building *ref_map* loci in STACKS is not very efficient, and loses too much data, which complicates the pipeline even more! Thus, the pipeline for *ref_map.pl*, using their so-called *"integrated"* method should be: 

	process_radtags #demultiplex
	denovo_map.pl #initial genotyping
	GSNAP or bwa #align raw reads to catalog loci from denovo
	integrate_alignments.py #integrate alignment information back into denovo ouput
	populations

So many steps!! 
	

Genotyping with denovo_map.pl
---


Let's make a list of the filenames that have sequences in them using the following command:

	cd demultiplex
	ls | awk '/fq/' > sequence_files.txt

This list of filenames will be a part of the input for running *denovo_map.pl*, since you have to list all of the sequence files that will be used for input, rather than a directory containing them. To learn more about **awk** basics, a very powerful tool for editing/rewriting text files, you can [start here](https://github.com/rdtarvin/IBS2019_Genomics-of-Biodiversity/blob/master/files/AWK-cheatsheet.md).

Let's start setting up denovo_map runs. Here is the general code we will use:

	mkdir denovo
	denovo_map.pl -T 2 -m 3 -M 2 -n 1 -o ./denovo --samples ./demultiplex --popmap epi_popmap.txt --paired
	
**Q: what does the backslash '\' mean here?**

The denovo code needs to have every single sequence that you will genotype listed in a single line. Thus, you need to build your **denovo_map** file with EVERY sequence that you will use separately.... **How should we do this?** 

OK, let's start **denovo_map**!!! Look at the terminal window as it runs.... what's happening currently...? While we wait, let's look more into the **STACKS** manual.

#####
#####


One thing that is very important in stacks is troubleshooting parameter settings. The defaults in STACKS are **NOT GOOD** to use, and depending on the specifics of the dataset (divergence, number of populations, samples, etc) these parameters will vary a lot from one study to the other. The main parameters to mess with are: 

	m — specify a minimum number of identical, raw reads required to create a stack.
	M — specify the number of mismatches allowed between reads when processing a single individual (default 2).
	n — specify the number of mismatches allowed between reads (among inds.) when building the catalog (default 1).

**Note 1**: The higher the coverage, the higher the m parameter can be. 

**Note 2**: M should not be 1 (diploid data) but also should not be very high since it will begin to stack paralogs. 

**Note 3**: n will depend on how divergent our individuals/populations are. It should not be zero, since that would essentially allow zero SNPs, but 1 also seems unrealistically low (only a single difference between individuals in any given locus), so in these kinds of datasets we should have permutations that start from 2.  If you use n 1 it is likely to oversplit loci among populations that are more divergent. 

The same paper that discussed the issues with *ref_map.pl* that I mentioned previously, also mentions some tips for picking the ideal parameter settings for stacks... but, in general my recommendation would be: explore your dataset!!! Some general suggestions from it: 

- Setting the value of *m* in essence is choosing how much "error" you will include/exclude from your dataset. This parameter creates a trade-off between including error and excluding actual alleles/polymorphism. Higher values of *m* increase the average sample coverage, but decreases the number of assembled loci. After m=3 loci number is more stable.
- Setting the value *M* is a trade-off between overmerging (paralogs) and undermerging (splitting) loci.  It is **VERY dataset-specific** since it depends on polymorphism in the species/populations and in the amount of error (library prep and sequencing). 
- Setting the value *n* is also critical when it comes to overmerging and undermerging loci. There seems to be an unlimited number of loci that can be merged with the catalog wiht increasing n!! 
- Finally, authors suggest that a general rule for setting parameters is n=M, n=M-1, or n=M+1, and that M is the main parameter that needs to be explored for each dataset. 



However, given that these methods are still very new and that we still don't know how to "Easily" and properly assess error, the more permutations you do with the parameter settings, the more you will understand what your dataset is like, and the better/more "real" your loci/alleles will be. Here are some recommended permutations to run wiht your dataset:

Permutations | -m | -M | -n | --max_locus_stacks 
------------ | ------------- | ------------ | ------------- | ------------ |
a | 3 | 2 | 2 | 3 | 
b | 5 | 2 | 2 | 3 |
c | 7 | 2 | 2 | 3 | 
d | 3 | 3 | 2 | 3 |
e | 3 | 4 | 2 | 3 |
f | 3 | 5 | 2 | 3 |
g | 3 | 2 | 3 | 3 |
h | 3 | 2 | 4 | 3 |
i | 3 | 2 | 5 | 3 |
j | 3 | 2 | 2 | 4 |
k | 3 | 2 | 2 | 5 |

You can evaluate the number of loci, SNPs, and Fsts that you get from these parameters to assess "stability" of genotyping and pick optimal parameter settings. 

**NOW BACK TO OUR GENOTYPING IN STACKS....**

#####

#####


Getting the output with **populations**
----

The final step in the stacks pipeline is to run the program **populations**. Similar to step 7 in ipyrad, it outputs/summarizes your data into formats you specify. However, another super nice thing about this program is that it runs populations stats for you and puts them in a nice excel-readable output!! :D yay easy pogen stats!!  

To run **populations**, we first need to develop a popmap file, which simply contains names of sequences (first column)and some population code (second column)that they belong to, tab delimited. Our sample/file names alrady contain the population information, so try to build it yourself.... how do you want to do it???

 

Now, let's run **populations** using the following command:

	populations -P ./denovo -M ./epi_popmap.txt -p 1 -r 0 --structure --genepop --vcf --phylip --fasta-samples-raw --phylip-var
	populations -P ./denovo -M ./epi_popmap_singleton.txt -p 1 -r 0 --structure --genepop --vcf --phylip --fasta-samples-raw --phylip-var
	
	python vcf2phylip.py -i ./denovo/populations.snps.vcf -m 1


Before we move on to the next steps.... let's [talk a bit](https://docs.google.com/presentation/d/1ZfCd0jIuNm4MwdCTw0MOXtyLBBlpRB3Xt_jHWhOcQhk/pub?start=false&loop=false&delayms=60000) about post-genotyping filters and the nature of RADseq datasets and SNP matrices... 


Post-filtering in **plink**
----
We are now going to filter our matrix to reduce biases and incorrect inferences due to missing data (in individuals and SNPs)and by Minor Allele Frequency. 


1. First, we filter loci with less than 60% individuals sequenced

		./plink --file filename --geno 0.4 --recode --out filename_a --noweb


2. Second, we filter individuals that have less than 50% data

		./plink --file filename_a --mind 0.5 --recode --out filename_b --noweb


3. Third, we filter loci with MAF < 0.02 in remaining individuals

		/.plink --file filename_b --maf 0.02 --recode --out filename_c --noweb


Second output from stacks *populations*
----

Now we are going to re-run the last step of the **STACKS** pipeline, so that we can get the nice population stats with out cleaner matrix. 

We need to make a ***whitelist*** file, which is a list of the loci to include based on the plink results (i.e. on amount of missing data in locus). The whitelist file format is ordered as a simple text file containing one catalog locus per line: 

		% more whitelist
		3
		7
		521
		11
		46
		103
		972
		2653
		22
		
		
In order to get from the .map file to the whitelist file format, open *_c.map file in Text Wrangler, and do find and replace arguments using **grep**:


	search for \d\t(\d*)_\d*\t\d\t\d*$
	replace with \1



Using the **.irem** file from the second iteration of *plink* (in our example named with termination **"_b"**), remove any individuals from the first popmap if they did not pass **plink** filters so that they are excluded from the analysis (i.e. individuals with too much missing data). 


Now we can run populations again using the whitelist of loci and the updated popmap file for loci and individuals to retain based on the plink filters.

	populations -b 1 -P ./ -M ./popmap.txt  -p 1 -r 0.5 -W Pr-whitelist --write_random_snp --structure --plink --vcf --genepop --fstats --phylip
	

We will use many of these outputs for downstream analyses. Outputs are: 

	batch_2.hapstats.tsv
	batch_2.phistats.tsv
	batch_2.phistats_1-2.tsv
	batch_2.phistats_1-3.tsv
	batch_2.phistats_2-3.tsv
	batch_2.sumstats.tsv
	batch_2.sumstats_summary.tsv
	batch_2.haplotypes.tsv
	batch_2.genepop
	batch_2.structure.tsv
	batch_2.plink.map
	batch_2.plink.ped
	batch_2.phylip
	batch_2.phylip.log
	batch_2.vcf
	batch_2.fst_1-2.tsv
	batch_2.fst_1-3.tsv
	batch_2.populations.log
	batch_2.fst_summary.tsv
	batch_2.fst_2-3.tsv



Copy scripts to your virtual machine Applications folder via git
```bash
cd ~/Applications
git clone https://github.com/z0on/2bRAD_denovo.git
ls
cd ../workshop/2bRAD/
```
Git is an important programming tool that allows developers to trace changes made in code. Let's take a look online.
```bash
sensible-browser https://github.com/z0on/2bRAD_denovo
```

Okay, before we start the pipeine let's move our fastqc files to their own directory
```bash
mkdir 2bRAD_fastqc
mv *fastqc* 2bRAD_fastqc # shows error stating that the folder couldn't be moved into the folder
ls # check that everything was moved
```

First we need to concatenate data that were run on multiple lanes.
- T36R59_I93_S27_L00**6**_R1_001.fastq and T36R59_I93_S27_L00**7**_R1_001.fastq
- pattern "T36R59_I93_S27_L00" is common to both read files; program concatenates into one file with (.+) saved as file name

```bash
perl ~/Applications/2bRAD_denovo/ngs_concat.pl fastq "(.+)_S27_L00" # this takes a few minutes so let's take a quick break while it does its thing.
head T36R59_I93.fq

@K00179:73:HJCTJBBXX:7:1101:28006:1209 1:N:0:TGTTAG
TNGTCCACAAGAGTGTGTCGAGCGTTGTGCCCCCCCGCATCTCTACAGAT
+
A#AAFAFJJJJJJJJJJJJJFJJJJJJFJJJJJJJJJJJFJFJJJJJAJ<
@K00179:73:HJCTJBBXX:7:1101:28026:1209 1:N:0:TGTTAG
CNAACCCGTTGTCACGTCGCAAATAAGTCGGTGCGCTGGCAATCACAGAT
+
A#AFFJJJFJJFFJJJJJJJJFFJJJJJFJFJFJFJJJJJJJJJJJJJJF
@K00179:73:HJCTJBBXX:7:1101:28047:1209 1:N:0:TGTTAG
GNGTCCCAGTGATCCGGAGCAGCGACGTCGCTGCTATCCATAGTGAAGAT
```

Now that our read files are concatenated, we need to separate our reads by barcode. 
Let's take a look again at the structure of a 2bRAD read.<br>

![](https://github.com/rdtarvin/RADseq_Quito_2017/blob/master/images/2bRAD-read.png?raw=true)


From the 2bRAD native pipeline we will use ```trim2bRAD_2barcodes_dedup2.pl``` script to separate by barcode. 
If your data are not from HiSeq4000 you would use ```trim2bRAD_2barcodes_dedup.pl```. This takes <10 min
```bash
# adaptor is the last 4 characters of the reads, here 'AGAT'
perl ~/Applications/2bRAD_denovo/trim2bRAD_2barcodes_dedup2.pl input=T36R59_I93.fq adaptor=AGAT sampleID=1
.
.
.
T36R59_ACCA: goods: 295784 ; dups: 1178405
T36R59_AGAC: goods: 260575 ; dups: 987301
T36R59_AGTG: goods: 325595 ; dups: 956574
T36R59_CATC: goods: 432507 ; dups: 1732082
T36R59_CTAC: goods: 311897 ; dups: 1837423
T36R59_GACT: goods: 322958 ; dups: 1877945
T36R59_GCTT: goods: 266101 ; dups: 1040723
T36R59_GTGA: goods: 483664 ; dups: 1871167
T36R59_GTGT: goods: 328948 ; dups: 1298015
T36R59_TCAC: goods: 274208 ; dups: 1494727
T36R59_TCAG: goods: 309572 ; dups: 1109505
T36R59_TGTC: goods: 310155 ; dups: 1800440

T36R59: total goods : 3921964 ; total dups : 17184307

```

You can see that there are a ton of duplicate reads in these files. This is OK and means that you have high 
coverage across loci. Don't confuse these duplicates with PCR duplicates, which may be a source of error (more on this later).

```bash
ls
```

Now you can see that the demultiplexed and deduplicated files are listed by barcode and have the file extension **.tr0**.


Step 2. Filter reads by quality with a program from the **fastx_toolkit**
---

```bash
fastq_quality_filter -h

# Use typical filter values, i.e., 90% of bases in a read should have a q-value aboce 20
# This is a for loop, which allows you to execute the same command with arguments across multiple files
# The 'i' variable is a place holder 
for i in *.tr0; do fastq_quality_filter -i $i -q 20 -p 90 > ${i}.trim; done

# zip the files to save space
for i in *.trim; do gzip ${i}; done
```

Now we have our 2bRAD reads separated by barcode and trimmed (steps 1 & 2)!<br>


**TASK**: The files need to be renamed for each species. 
Using the barcode file [here](https://raw.githubusercontent.com/rdtarvin/RADseq_Quito_2017/master/files/2bRAD-ipyrad_barcodes.txt) and the command `mv`, 
rename all .gz files to have the format `genX_spX-X_R1_.fastq.gz`.<br>



Ok this is all great but there isn't much of a point to work bioinformatically with the files in their unzipped (large) format. So let's rezip them.

```bash
gzip *.fastq
```

There are actually several ways to look at .gz files, such as:
```
zless epiddrad_t200_R1_.fastq.gz # press 'q' to exit
gzcat epiddrad_t200_R1_.fastq.gz | head # the "|" pipes stdout to the program "head"
gzcat epiddrad_t200_R1_.fastq.gz | head -100 # shows the first 100 lines
```
