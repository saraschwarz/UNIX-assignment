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
### fang_et_al_genotypes.txt
### snp_position.txt
