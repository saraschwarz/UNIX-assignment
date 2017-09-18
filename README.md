# UNIX-assignment
## Data Inspection
### fang_et_al_genotypes.txt
- $ wc fang_et_al_genotypes.txt
	* 2783 lines
	* 2744038 words
	* 11051939 characters
- $ du -h fang_et_al_genotypes.txt
	* size of text file - 11M
- $ awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt
	* 986 columns
- $ file fang_et_al_genotypes.txt
	* ASCII text, with very long lines
### snp_position.txt
- $ wc snp_position.txt
	* 984 lines
	* 13198 words
	* 82763 characters
- $ du -h snp_position.txt
	* size of text file - 84K
- $ awk -F "\t" '{print NF; exit}' snp_position.txt
	* 15 comlumns
- $ file snp_position.txt
	* ASCII text
## Data Processing
### fang_et_al_genotypes.txt
### snp_position.txt
