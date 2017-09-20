# UNIX-assignment
## Data Inspection
### fang_et_al_genotypes.txt
#### Word count code: lists lines, words, and characters in file
- $ wc fang_et_al_genotypes.txt
	* 2783 lines
	* 2744038 words
	* 11051939 characters
#### File size code: lists file size in human readable format (-h)
- $ du -h fang_et_al_genotypes.txt
	* size of text file - 11M
#### Counting columns: awk one liner that more accurately counts columns than head command
- $ awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt
	* 986 columns
#### Identification of ASCII characters
- $ file fang_et_al_genotypes.txt
	* ASCII text, with very long lines
### snp_position.txt
#### Word count code: lists lines, words, and characters in file
- $ wc snp_position.txt
	* 984 lines
	* 13198 words
	* 82763 characters
#### File size code: lists file size in human readable format (-h)
- $ du -h snp_position.txt
	* size of text file - 84K
#### Counting columns: awk one liner that more accurately counts columns than head command
- $ awk -F "\t" '{print NF; exit}' snp_position.txt
	* 15 comlumns
#### Identification of ASCII characters
- $ file snp_position.txt
	* ASCII text
## Data Processing
### Teosinte Data
#### **Pull out teosinte groups from main combined file (fang)**
- $ grep -E "(ZMPBA|ZMPIL|ZMPJA)" fang_et_al_genotypes.txt > teosinte_genotypes.txt
#### **Put headers saved from maize file into group file**
- $ cat maize_header teosinte_genotypes.txt > teosinte_genotypes_header.txt
#### **Double check number of columns after pull and adding headers**
- $ awk -F "\t" '{print NF; exit}' teostinte_genotypes_header.txt
#### **Transpose teosinte genotypes before sorting and joining to snps files**
- $ awk -f transpose.awk teosinte_genotypes_header.txt > transposed_teosinte_genotypes.txt
#### **Sort teosinte genotype file by snp locations without headers**
- $ tail -n +4 transposed_teosinte_genotypes.txt | sort -k1,1 > teosinte_genotypes_sorted.txt
#### **Join teosinte and snp position files**
- $ join -t '\t' -1 1 -2 1 snp_positions_sorted.txt teosinte_genotypes_sorted.txt > joined_teosinte.txt
#### **Add headers to joined teosinte file**
- $ cat snp_headers joined_teosinte.txt > joined_teosinte_header.txt
#### **Cut and save SNP ID, chromosome, and position columns**
- $ cut -f 1,3,4 joined_teosinte_header.txt > joined_teosinte_columns.txt
#### **Separate chromosome files for teosinte**
- $ for i in {1..10}; do awk '$2=='$i'' joined_teosinte_columns.txt > chr"$i"_teosinte_genotypes_final.txt; done
#### **Sort all teosinte chromosome files by increasing position**
- $ for i in {1..10}; do sort -k3,3n chr"$i"_teosinte_genotypes_final.txt > chr"$i"_teosinte_genotypes_increasing.txt; done
#### **Sort all teosinte files by decreasing position**
- $ for i in {1..10}; do sort -k3,3nr chr"$i"_teosinte_genotypes_final.txt > chr"$i"_teosinte_genotypes_decreasing.txt; done
#### **Replace all "?" with "-" in decreasing position files**
- $ for i in {1..10}; do sed 's/?/-/g' chr"$i"_teosinte_genotypes_decreasing.txt > chr"$i"_teosinte_genotypes_replace.txt; done
#### **Creating file for unknowns for teosinte**
- $ grep "unknown" joined_teosinte_columns.txt > unknown_teosinte.txt
#### **Creating file for multiple unknown positions**
- $ grep "multiple" joined_teosinte_columns.txt > multiple_teosinte.txt
### Maize Data
#### **Pull out maize groups from main combined file (fang)**
- $ grep _ "(ZMMIL|ZMMLR|ZMMMR)" fang_et_al_genotypes.txt > maize_genotypes.txt
#### **Pull headers so they can be added to new maize and teosinte group files**
- $ head -n 1 fang_et_al_genotypes.txt > maize_header
#### **Add headers to new maize group file**
- $ cat maize_header maize_genotypes.txt > maize_genotypes_header.txt
#### **Double check number of columns after pull and adding headers**
- $ awk -F "\t" '{print NF; exit}' maize_genotypes_header.txt
#### **Transpose maize genotypes before sorting and joining to snps files**
- $ awk -f transpose.awk maize_genotypes_header.txt > transposed_maize genotypes.txt
#### **Sort maize group file by snp locations without headers**
- $ tail -n +4 transposed_maize_genotypes.txt | sort -k1,1 > maize_genotypes_sorted.txt
#### **Save snp headers so they can be added to joined file**
- $ head -n 1 snp_position.txt > snp_headers
#### **Sort snp positions file without headers**
- $ tail -n +2 snp_position.txt | sort -k1,1 > snp_positions_sorted.txt
#### **Join maize and snp files**
- $ join -t $'\t' -1 1 -2 1 snp_positions_sorted.txt maize_genotypes_sorted.txt > joined_maize.txt
#### **Add headers to joined file so correct columns can be cut**
- $ cat snp_headers joined_maize.txt > final_maize.txt
#### **Cut and save SNP ID, Chromosome, and Position columns**
- $ cut -f 1,3,4 final_maize.txt > columns_maize.txt
#### **Separate maize files based on chromosome**
- $ for i in {1..10}; do awk '$2=='$i''columns_maize.txt > chr"$i"_maize_genotypes_final.txt; done
#### **Sort each chromosome file by increasing position for maize**
- $ for i in {1..10}; do sort -k3,3n chr"$i"_maize_genotypes_final.txt > chr"$i"_maize_genotypes_increasing.txt; done
#### **Sort each chromosome file by decreasing position for maize**
- $ for i in {1..10}; do sort -k3,3nf chr"$i"_maize_genotypes_final.txt > chr"i"_maize_genotypes_decreasing.txt; done
#### **Replace all "?" with "-" in the decreasing position files**
- $ for i in {1..10}; do sed 's/?/-/g' chr"$i"_maize_genotypes_decreasing.txt > chr"$i"_maize_genotypes_replace.txt
#### **Creating file for unknown positions for maize**
- $ grep "unknown" columns_maize.txt > unknown_maize.txt
#### **Creating file for multiple unknown positions**
- $ grep "multiple" columns_maize.txt > multiple_maize.txt




