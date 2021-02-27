#UNIX Assignment - *Lori Croghan*

##Data Inspection

###Attributes of `fang_et_al_genotypes.txt`

**Code used for inspecting this data file:**

```
head fang_et_al_genotypes.txt

head -n 1 fang_et_al_genotypes.txt

tail -n 3 fang_et_al_genotypes.txt

wc -l fang_et_al_genotypes.txt

du -h fang_et_al_genotypes.txt

awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt

-n 2 fang_et_al_genotypes.txt | awk -F "\t" '{print NF; exit}'

file fang_et_al_genotypes.txt 

cut -f 1-10 fang_et_al_genotypes.txt | head -n 10

	*and different variations (tail/different numbers) of this last command to view the file structure*
```

**By inspecting this file I learned that:**

1. There are many rows and columns to the file that make it difficult to view

2. The header includes columns like Sample_ID and is quite long

3. The end of the file contains genome data in the X/X format

4. There are 2,783 lines/rows in the file  

5. The file is 6.1 Mb large

6. There are 986 columns in the first line and throughout the file

7. All the text in the file is ASCII format


###Attributes of `snp_position.txt`

**Code used for inspecting this data file:**

```
head snp_position.txt

head -n 1 snp_position.txt

tail -n 3 snp_position.txt

wc -l snp_position.txt

du -h snp_position.txt

awk -F "\t" '{print NF; exit}' snp_position.txt

-n 2 snp_position.txt | awk -F "\t" '{print NF; exit}'

file snp_position.txt

cut -f 1-10 snp_position.txt | head -n 10

        *and different variations (tail/different numbers) of this last command to view the file structure*
```

**By inspecting this file I learned that:**

1. This file initially looks smaller due to there being less columns

2. The header has the first column as "SNP_ID" and other columns labeled for chromosome number and position

3. I noticed that the first column of `snp_position.txt` matches up with the first line of `fang_et_al_genotypes`

4. There are 984 lines/rows in the file

5. The file is 38 Kb large

6. There are 15 columns in the first line and throughout the file

7. All the text in the file is ASCII format


##Data Processing


###Maize Data

