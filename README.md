## Johnathon Shook- UNIX

## Data Inspection
--> $ for filename in fang_et_al_genotypes.txt snp_position.txt ; do echo "Number of lines: $(wc -l $filename)"; echo  "Number of columns: $(awk -F "\t" '{print NF; exit}' $filename) $filename"; echo "File size: $(du -h $filename)"; done

**Output:**

Number of lines: 2783 fang_et_al_genotypes.txt

Number of columns: 986 fang_et_al_genotypes.txt

File size: 11M       fang_et_al_genotypes.txt

Number of lines: 984 snp_position.txt

Number of columns: 15 snp_position.txt

File size: 84K       snp_position.txt

## Data Processing
## Split into separate maize and teosinte files

--> $ grep -E "(ZMMIL|ZMMLR|ZMMMR)" fang_et_al_genotypes.txt > maize_genotypes.txt


--> $ grep -E "(ZMPBA|ZMPIL|ZMPJA)" fang_et_al_genotypes.txt > teosinte_genotypes.txt

## Create file w/ headers from the genotype file and add it back to the extracted files

--> $ grep "Group" fang_et_al_genotypes.txt > header.txt

--> $ cat header.txt maize_genotypes.txt > maize_header.txt 

--> $ cat header.txt teosinte_genotypes.txt > teosinte_header.txt

## Remove first 2 columns so column *(SNP ID)* can be used to join the files

--> $ cut -f 3-968 maize_header.txt > maize_cut.txt 

--> $ cut -f 3-968 teosinte_header.txt > teosinte_cut.txt

## Transpose the data to allow genotypes and snp files to merge

--> $ awk -f transpose.awk maize_cut.txt > transposed_maize.txt

--> $ awk -f transpose.awk teosinte_cut.txt > transposed_teosinte.txt

## Keep only columns 1, 3 and 4 from snp.position.txt file

--> $ grep -v "^#" snp_position.txt | cut -f 1,3,4 > snp_position_cut.txt

## Remove headers from the files

--> $ grep -v "Group" transposed_maize.txt > maize_no_header.txt

--> $ grep -v "Group" transposed_teosinte.txt > teosinte_no_header.txt 

--> $ grep -v "SNP_ID" snp_position.txt_cut > snp_no_header.txt

## Sort both Genotype and SNP files to appropriately join them 

--> $ sort -k1,1 snp_no_header.txt > snp_sorted.txt 

--> $ sort -k1,1 maize_no_header.txt > maize_sorted.txt

-> $ sort -k1,1 teosinte_no_header.txt > teosinte_sorted.txt

## Join SNP and Genotype files

--> $ join -t $'\t' -1 1 -2 1 snp_sorted.txt maize_sorted.txt > maize_joined.txt

--> $ join -t $'\t' -1 1 -2 1 snp_sorted.txt teosinte_sorted.txt > teosinte_joined.txt

## Sort files by chromosome number

$ sort -k2,2n maize_joined.txt > maize_sorted_by_chr.txt 

$ sort -k2,2n teosinte_joined.txt > teosinte_sorted_by_chr.txt

## Code missing data as a dash instead of question mark

--> $ sed 's/?/-/g' maize_sorted_by_chr.txt > maize_dash.txt

--> $ sed 's/?/-/g' teosinte_sorted_by_chr.txt > teosinte_dash.txt

## Create separate files for each chromosome

--> $ for i in {1..10}; do awk '$2=='$i'' maize_sorted_by_chr.txt > maize_chr"$i"_questionmark.txt; done

--> $ for i in {1..10}; do awk '$2=='$i'' teosinte_sorted_by_chr.txt > teosinte_chr"$i"_questionmark.txt; done

--> $ for i in {1..10}; do awk '$2=='$i'' maize_dash.txt > maize_chr"$i"_dash.txt; done

--> $ for i in {1..10}; do awk '$2=='$i'' teosinte_dash.txt > teosinte_chr"$i"_dash.txt; done

## Sort files with missing data encoded by ? based on increasing SNP position values

--> $ for i in {1..10}; do sort -k3,3n maize_chr"$i"_questionmark.txt > maize_chr"$i"_questionmark_ordered.txt; done

--> $ for i in {1..10}; do sort -k3,3n teosinte_chr"$i"_questionmark.txt> teosinte_chr"$i"_questionmark_ordered.txt; done

## Sort files with missing data encoded by - based on decreasing SNP position values

--> for i in {1..10}; do sort -k3,3nr maize_chr"$i"_dash.txt > maize_chr"$i"_dash_ordered.txt; done

--> $ for i in {1..10}; do sort -k3,3nr teosinte_chr"$i"_dash.txt > teosinte_chr"$i"_dash_ordered.txt; done

## Create a file with all SNPs with unknown position in the genome

--> $ grep "unknown" maize_sorted_by_chr.txt > maize_unknown.txt

--> $ grep "unknown" teosinte_sorted_by_chr.txt > teosinte_unknown.txt

## Create a file with all SNPs with multiple position in the genome

--> $ grep "multiple" maize_sorted_by_chr.txt > maize_multiple.txt

--> $ grep "multiple" teosinte_sorted_by_chr.txt > teosinte_multiple.txt

## Stage and Commit changes

--> $ git add . 

--> $ git commit -m "Unix Assignment" 

--> $ git push origin master


# jmshook
