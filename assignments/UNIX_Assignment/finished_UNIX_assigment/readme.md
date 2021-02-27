# UNIX Assignment - *Lori Croghan*

## Data Inspection

### Attributes of `fang_et_al_genotypes.txt`

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
```

	*and different variations (tail/different numbers) of this last command to view the file structure*

**By inspecting this file I learned that:**

1. There are many rows and columns to the file that make it difficult to view

2. The header includes columns like Sample_ID and is quite long

3. The end of the file contains genome data in the X/X format

4. There are 2,783 lines/rows in the file  

5. The file is 6.1 Mb large

6. There are 986 columns in the first line and throughout the file

7. All the text in the file is ASCII format


### Attributes of `snp_position.txt`

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
```

        *and different variations (tail/different numbers) of this last command to view the file structure*

**By inspecting this file I learned that:**

1. This file initially looks smaller due to there being less columns

2. The header has the first column as "SNP_ID" and other columns labeled for chromosome number and position

3. I noticed that the first column of `snp_position.txt` matches up with the first line of `fang_et_al_genotypes`

4. There are 984 lines/rows in the file

5. The file is 38 Kb large

6. There are 15 columns in the first line and throughout the file

7. All the text in the file is ASCII format



## Data Processing


### Maize Data

```
grep -E "(ZMMLR|ZMMIL|ZMMMR)" fang_et_al_genotypes.txt > maize_fang_genotype.txt
```

This extracted the maize data and created a new file

```
grep -E “(Sample_ID)” fang_et_al_genotypes.txt > headerfang.txt
```
	
This created a new file with just the header of fang_et_al_genotypes.txt 

```
cat header_fang.txt maize_fang_genotype.txt > maize_fang_genotype_incl_header.txt
```

Added the header back onto the maize data

```
awk -f transpose.awk maize_fang_genotype_incl_header.txt > transposed_maize_genotypes.txt
```

Transposed the maize data so that a `join` will be possible

```
sort -k1,1 transposed_maize_genotypes.txt > sorted_transposed_maize_genotypes.txt
```

Sorted the maize data to prepare for a join

```
sort -k1,1 snp_position.txt > sorted_snp_position.txt
```

Sorted `snp_position.txt` file to prepare for a join

```
join -1 1 -2 1 -t $'\t' sorted_snp_position.txt sorted_transposed_maize_genotypes.txt > joined_maize.txt
```

Joined the two files together

```
sort -k3,3 joined_maize.txt > sorted_joined_maize.txt
```

Sorted the file alphanumerically by chromosome number (third column)

```
awk '$3 == "1"' sorted_joined_maize.txt > chr1_maize.txt
```

Created a file with maize data of only chromosome 1

*Repeated this sequence for each chromosome by replacing "1" and "chr1" for each chromosome number*

```
sort -k4,4 -n chr1_maize.txt > chr1_increasing_maize.txt
```

Sorted the data by order of increasing snp position (column 4)

*Repeated this sequence for each chromosome by replacing "chr1" for each chromosome number*

**This step created the final files named chrX_increasing_maize.txt**

```
sort -k4,4 -r -n chr1_maize.txt > chr1_decreasing_maize.txt
```

Sorted the data by order of decreasing snp position (column 4)

*Repeated this sequence for each chromosome by replacing "chr1" for each chromosome number*

```
sed 's/?/-/g' chr*_decreasing*
```

Found and replaced all of the "?" with "-"

**This step created the final files named chrX_decreasing_maize.txt**

### Teosinte Data

```
grep -E "(ZMPJA|ZMPIL|ZMPBA)" fang_et_al_genotypes.txt > teosinte_fang_genotype.txt
```

This extracted the teosinte data and created a new file

```
grep -E “(Sample_ID)” fang_et_al_genotypes.txt > headerfang.txt
```

This created a new file with just the header of fang_et_al_genotypes.txt

```
cat header_fang.txt teosinte_fang_genotype.txt > teosinte_fang_genotype_incl_header.txt
```

Added the header back onto the teosinte data

```
awk -f transpose.awk teosinte_fang_genotype_incl_header.txt > transposed_teosinte_genotypes.txt
```

Transposed the teosinte data so that a `join` will be possible

```
sort -k1,1 transposed_teosinte_genotypes.txt > sorted_transposed_teosinte_genotypes.txt
```

Sorted the teosinte data to prepare for a join

```
sort -k1,1 snp_position.txt > sorted_snp_position.txt
```

Sorted `snp_position.txt` file to prepare for a join

```
join -1 1 -2 1 -t $'\t' sorted_snp_position.txt sorted_transposed_teosinte_genotypes.txt > joined_teosinte.txt
```

Joined the two files together

```
sort -k3,3 joined_teosinte.txt > sorted_joined_teosinte.txt
```

Sorted the file alphanumerically by chromosome number (third column)

```
awk '$3 == "1"' sorted_joined_teosinte.txt > chr1_teosinte.txt
```

Created a file with maize data of only chromosome 1

*Repeated this sequence for each chromosome by replacing "1" and "chr1" for each chromosome number*

```
sort -k4,4 -n chr1_teosinte.txt > chr1_increasing_teosinte.txt
```

Sorted the data by order of increasing snp position (column 4)

*Repeated this sequence for each chromosome by replacing "chr1" for each chromosome number*

**This step created the final files named chrX_increasing_teosinte.txt**

```
sort -k4,4 -r -n chr1_teosinte.txt > chr1_decreasing_teosinte.txt
```

Sorted the data by order of decreasing snp position (column 4)

*Repeated this sequence for each chromosome by replacing "chr1" for each chromosome number*

```
sed 's/?/-/g' chr*_decreasing*
```

Found and replaced all of the "?" with "-"

**This step created the final files named chrX_decreasing_teosinte.txt**

