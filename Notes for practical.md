
### Notes for Practical #1

**Forking and Cloning a Repository**
1. Open the repository and hit fork button
2. Go to own GitHub page, overview, repositories
3. Open forked repository, click on it, click '<>Code' button, copy HTTPS address of the clone
4. Open a terminal connected to RON in vscode
5. enter git clone https://github.com/USERNAME/reponame.git
6. Use ls to confirm the clone

**3 ways to Change Directories to Home**
1. cd $HOME
2. cd ~
3. cd ../../../

**How to list files in /bin starting with certain letters**

```
ls /bin/c* ls /bin/ | grep '^c'
```

**Command to find the line number in your history**

```
ls /bin/c* | ws -l
```

**How to navigate to home and list contents of a directory from there**

```
ls -F gen711-811/shell_data/untrimmed_fastq/
```

**Navigate to a directory an list hidden directories**
1. ls --all .hidden/
2. ls -a
3. ls -la
4. ls -laF (long format, include security settings for files)
5. ls .*

**Find the line number in your history for the command that listed .sh files in /user/bin**
1. ls /usr/bin/*.sh
2. ls /usr/binc* | wc -l

**Print out the contents of a .fastq file, find the last line**
1. cat NAME.fastq
2. tail -n1 NAME.fastq (or use -n4 if you want the full read of fastq file)

* To view the first lines instead of the last

```
head -n4 NAME.fastq
```

**In a .fastq file, find the next nucleotides after the first instance of TTTT**
1. less NAME.fasta 
2. less -S NAME.fasta /TTTT
3. grep 'TTTT' *fastq

**Format of file permissions**
* (file type)(user)(group)(other)
* rwx is read, write, execute permissions

**View and change file permissions**
* use command below to view

```
ls -l
```

* use command below to change permissions

```
chmod (permission) FILE.fastq
```

* adding -w will make the file write-protected
* adding ug+rwx specifies user and group and gives rwx permissions

**Create backups of fastq files**
1. mkdir backup
2. cp NAMEofFILE NEWNAMEofCOPY
3. mc *backup.fastq backup/

**How to find size of fastq file**

```
ls -l -h
```

**Load a conda environment and find where a program called 'fastqc' is stored**
1. activate genomics (this loads conda called genomics)

```
fastqc *.fastq
```

**Unzip a zipped file**

```
*zip
```

**Searcing within a file using combined commands**

```
grep -A1 -h '@SRR' *fastq
```

* above command searches files ending in fastq with the header line @SRR, -A1 displays one line after each match, -h suppresses names

```
grep -A1 -h '@SRR' *fastq | grep -v '^--' | grep -v '^@SRR'
```

**Search a fastq file for a nucleotide sequence and return matching lines with the name for each sequence**
* use command below for a single specific file

```
grep -B1 "GNATNAC" NAME.fastq (for a single specific file)
```

*use command below to search all fastq files

```
grep -B "GNATNAC" *.fastq (to search all fastq files)
```

**Make a file called 'bad-read.fastq' made up of poor fastq reads**

```
grep -B1 -A2 'NNNNNNNNNN' NAME.fastq > bad-reas.fastq
```

**How many sequences are there in NAME.fastq file, considering there are 4 lines per sequence**

```
wc -l NAME.fastq
```

* divide the count by 4

**Find how many sequences are in a fastq file with at least 3 consecutive Ns**

```
grep NNN NAME.fastq | wc -l
```

**Remove _2026 from all .txt files**

```
for filename in *.fasta

do

echo -e name=$ (basename ${filename}.fastq)

echo -e mv ${filename} ${name}_2026.tx

done
```

**When wanting the script to tell us when it's done**

* below is the same as saying echo NAME.fastq echo NAME2.fastq

```
for name in *.fastq

do

echo ${name}

done
```

```
for fq in *.fastq

do

wc -l ${fq}

done
```

```
for filenmae in *.fastq

do

head -n 2 ${filename}

done
```

**Based on metadata, how many different generations exist in the data**

```
cut -f2 -d',' Ecoli_metadata_compoite.csv | sort | uniq | grep -v 'gen' | wc -l
```

* -f2 refers to the column that contains generations, -d refers to what pint the data is being considered up to, the file name with the data is listed, unique 'gen' is being searched for 

**Based on metadata, how many rows and columns are in this data**

```
head -n1 Ecoli_metadata_composite.csv | tr ',' '\n' | wc -l
```

**Based on metadata, how many citrate+ mutants have been recorded in Ara-3?**

```
cut -f12 -d',' Ecoli_metadata_composite.csv | sort | uniq -c
```

**Based on metadata, how many hypermutable mutants have been recorded in Ara-3**

```
grep 'plus' Ecoli_metadata_composite.csv | wc -l

cut -f6 -d',' Ecoli_metadata_composite.csv | sort | uniq -c

```

**From the home directory, make a new directory called 'name'**

```
mkdir ~/name
```

**Command to copy a fastq file named Sample1.fasta into a directory called 'name' without changing current directory**

Create separate copy of file, then move to 'name' directory

```
cp Sample1.fastq Sample1COPY.fastq

mc *COPY.fastq name/
```
Directly copy into directory

```
cp [absolute path to source files]Sample1.fastq name/
```

**Absolute path to change current working directory to 'name' folder/directory***

* Fill in '...' with directory path
```
cd /home/username/..../name
```

**When making new fasta files from fastq files**
1. view first two lines of fastq reads (header & sequence)
2. get rid of separators 
3. Redirect output in new files with a different extensions

```
grep -A 1 --no-group-separator  "@SRR09" filename.fastq > newfile.fasta
```

**Command to search how many reads have 15 or more uncalled bases in multiple samples and count the number of reads without making a new file**

```
grep 'NNNNN' *.fastq | wc -l
```

**Command to make a new directory called 'name' in current directory, then move fasta files in**

```
mkdir name

mv Sample1.fasta Sample2.fasta name/
```
**Without changing directories, command to confirm files made it into 'name' folder**

* general list

```
ls name
```

* detailed list

```
ls -l name
```

**Command to see 100th line of a file**

```
head -n 100 Sample1.fasta | tail -n 1
```

**Run (command) on Sample1.fasta, run again and redirect output to a new file**

```
md5sum Sample1.fasta > my_md5sums.txt
```

**Add a line of text to the end of an existing text file**

```
echo "Rachael" >> filename.txt
```