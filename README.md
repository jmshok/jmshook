## Johnathon Shook- UNIX

## Data inspection

$ du -h fang_et_al_genotypes.txt snp_position.txt

$ wc -l fang_et_al_genotypes.txt snp_position.txt

$ awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt

$ awk -F "\t" '{print NF; exit}' snp_position.txt

## Data processing

$ grep -E "(ZMMIL|ZMMLR|ZMMMR)" fang_et_al_genotypes.txt > maize_genotypes.txt

$ grep -E "(ZMPBA|ZMPIL|ZMPJA)" fang_et_al_genotypes.txt > teosinte_genotypes.txt

$ grep "Group" fang_et_al_genotypes.txt > header.txt

$ cat header.txt maize_genotypes.txt > maize.txt 

$ cat header.txt teosinte_genotypes.txt > teosinte.txt

$ cut -f 3-968 maize.txt > cut_maize.txt 

$ cut -f 3-968 teosinte.txt > cut_teosinte.txt

$ awk -f transpose.awk cut_maize.txt > transposed_maize.txt

$ awk -f transpose.awk cut_teosinte.txt > transposed_teosinte.txt

$ grep -v "^#" snp_position.txt | cut -f 1,3,4 > cut_snp_position.txt

$ grep -v "Group" transposed_maize.txt > maize_noheader.txt 

$ grep -v "Group" transposed_teosinte.txt > teosinte_noheader.txt 

$ grep -v "SNP_ID" cut_snp_position.txt > snp_noheader.txt

$ sort -k1,1 snp_noheader.txt > sorted_snp.txt 

$ sort -k1,1 maize_noheader.txt > sorted_maize.txt 

$ sort -k1,1 teosinte_noheader.txt > sorted_teosinte.txt

$ sort -k1,1 -c sorted_snp.txt | echo $? 

$ sort -k1,1 -c sorted_maize.txt | echo $?

$ sort -k1,1 -c sorted_teosinte.txt | echo $?

$ join -t $'\t' -1 1 -2 1 sorted_snp.txt sorted_maize.txt > maize_data.txt

$ join -t $'\t' -1 1 -2 1 sorted_snp.txt sorted_teosinte.txt > teosinte_data.txt

$ sort -k2,2n maize_data.txt > maize_sorted_by_chr.txt 

$ sort -k2,2n teosinte_data.txt > teosinte_sorted_by_chr.txt

$ sed 's/<TAB>/?/g' maize_sorted_by_chr.txt > maize_substituted.txt

$ sed 's/<TAB>/?/g' teosinte_sorted_by_chr.txt > teosinte_substituted.txt

$ sed 's/?/-/g' maize_substituted.txt > maize_substituted_dash.txt

$ sed 's/?/-/g' teosinte_substituted.txt > teosinte_substituted_dash.txt

$ awk '$2 == /1/' maize_substituted.txt > maize_chr1.txt

$ awk '$2 ~ /2/' maize_substituted.txt > maize_chr2.txt 

$ awk '$2 ~ /3/' maize_substituted.txt > maize_chr3.txt 

$ awk '$2 == /4/' maize_substituted.txt > maize_chr4.txt

$ awk '$2 ~ /5/' maize_substituted.txt > maize_chr5.txt 

$ awk '$2 ~ /6/' maize_substituted.txt > maize_chr6.txt 

$ awk '$2 == /7/' maize_substituted.txt > maize_chr7.txt

$ awk '$2 ~ /8/' maize_substituted.txt > maize_chr8.txt 

$ awk '$2 ~ /9/' maize_substituted.txt > maize_chr9.txt 

$ awk '$2 == /10/' maize_substituted.txt > maize_chr10.txt

$ awk '$2 ~ /1/' teosinte_substituted.txt > teosinte_chr1.txt 

$ awk '$2 ~ /2/' teosinte_substituted.txt > teosinte_chr2.txt 

$ awk '$2 == /3/' teosinte_substituted.txt > teosinte_chr3.txt

$ awk '$2 ~ /4/' teosinte_substituted.txt > teosinte_chr4.txt 

$ awk '$2 ~ /5/' teosinte_substituted.txt > teosinte_chr5.txt 

$ awk '$2 == /6/' teosinte_substituted.txt > teosinte_chr6.txt

$ awk '$2 ~ /7/' teosinte_substituted.txt > teosinte_chr7.txt 

$ awk '$2 ~ /8/' teosinte_substituted.txt > teosinte_chr8.txt 

$ awk '$2 == /9/' teosinte_substituted.txt > teosinte_chr9.txt

$ awk '$2 ~ /10/' teosinte_substituted.txt > teosinte_chr10.txt 

$ awk '$2 == /1/' maize_substituted_dash.txt > maize_chr1_dash.txt

$ awk '$2 ~ /2/' maize_substituted_dash.txt > maize_chr2_dash.txt 

$ awk '$2 ~ /3/' maize_substituted_dash.txt > maize_chr3_dash.txt 

$ awk '$2 == /4/' maize_substituted_dash.txt > maize_chr4_dash.txt

$ awk '$2 ~ /5/' maize_substituted_dash.txt > maize_chr5_dash.txt 

$ awk '$2 ~ /6/' maize_substituted_dash.txt > maize_chr6_dash.txt 

$ awk '$2 == /7/' maize_substituted_dash.txt > maize_chr7_dash.txt

$ awk '$2 ~ /8/' maize_substituted_dash.txt > maize_chr8_dash.txt 

$ awk '$2 ~ /9/' maize_substituted_dash.txt > maize_chr9_dash.txt 

$ awk '$2 == /10/' maize_substituted_dash.txt > maize_chr10_dash.txt

$ awk '$2 ~ /1/' teosinte_substituted_dash.txt > teosinte_chr1_dash.txt 

$ awk '$2 ~ /2/' teosinte_substituted_dash.txt > teosinte_chr2_dash.txt 

$ awk '$2 == /3/' teosinte_substituted_dash.txt > teosinte_chr3_dash.txt

$ awk '$2 ~ /4/' teosinte_substituted_dash.txt > teosinte_chr4_dash.txt 

$ awk '$2 ~ /5/' teosinte_substituted_dash.txt > teosinte_chr5_dash.txt 

$ awk '$2 == /6/' teosinte_substituted_dash.txt > teosinte_chr6_dash.txt

$ awk '$2 ~ /7/' teosinte_substituted_dash.txt > teosinte_chr7_dash.txt 

$ awk '$2 ~ /8/' teosinte_substituted_dash.txt > teosinte_chr8_dash.txt 

$ awk '$2 == /9/' teosinte_substituted_dash.txt > teosinte_chr9_dash.txt

$ awk '$2 ~ /10/' teosinte_substituted_dash.txt > teosinte_chr10_dash.txt 

$ sort -k3,3n maize_chr1.txt > maize_snp_chr1.txt 

$ sort -k3,3n teosinte_chr1.txt > teosinte_snp_chr1.txt

$ sort -k3,3nr maize_chr1_dash.txt > maize_snp_chr1_reversed.txt 

$ sort -k3,3nr teosinte_chr1_dash.txt > teosinte_snp_chr1_reversed.txt

$ sort -k3,3n maize_chr2.txt > maize_snp_chr2.txt 

$ sort -k3,3n teosinte_chr2.txt > teosinte_snp_chr2.txt

$ sort -k3,3nr maize_chr2_dash.txt > maize_snp_chr2_reversed.txt 

$ sort -k3,3nr teosinte_chr2_dash.txt > teosinte_snp_chr2_reversed.txt

$ sort -k3,3n maize_chr3.txt > maize_snp_chr3.txt 

$ sort -k3,3n teosinte_chr3.txt > teosinte_snp_chr3.txt

$ sort -k3,3nr maize_chr3_dash.txt > maize_snp_chr3_reversed.txt 

$ sort -k3,3nr teosinte_chr3_dash.txt > teosinte_snp_chr3_reversed.txt

$ sort -k3,3n maize_chr4.txt > maize_snp_chr4.txt 

$ sort -k3,3n teosinte_chr4.txt > teosinte_snp_chr4.txt

$ sort -k3,3nr maize_chr4_dash.txt > maize_snp_chr4_reversed.txt 

$ sort -k3,3nr teosinte_chr4_dash.txt > teosinte_snp_chr4_reversed.txt

$ sort -k3,3n maize_chr5.txt > maize_snp_chr5.txt 

$ sort -k3,3n teosinte_chr5.txt > teosinte_snp_chr5.txt

$ sort -k3,3nr maize_chr5_dash.txt > maize_snp_chr5_reversed.txt 

$ sort -k3,3nr teosinte_chr5_dash.txt > teosinte_snp_chr5_reversed.txt

$ sort -k3,3n maize_chr6.txt > maize_snp_chr6.txt 

$ sort -k3,3n teosinte_chr6.txt > teosinte_snp_chr6.txt

$ sort -k3,3nr maize_chr6_dash.txt > maize_snp_chr6_reversed.txt 

$ sort -k3,3nr teosinte_chr6_dash.txt > teosinte_snp_chr6_reversed.txt

$ sort -k3,3n maize_chr7.txt > maize_snp_chr7.txt 

$ sort -k3,3n teosinte_chr7.txt > teosinte_snp_chr7.txt

$ sort -k3,3nr maize_chr7_dash.txt > maize_snp_chr7_reversed.txt 

$ sort -k3,3nr teosinte_chr7_dash.txt > teosinte_snp_chr7_reversed.txt

$ sort -k3,3n maize_chr8.txt > maize_snp_chr8.txt 

$ sort -k3,3n teosinte_chr8.txt > teosinte_snp_chr8.txt

$ sort -k3,3nr maize_chr8_dash.txt > maize_snp_chr8_reversed.txt 

$ sort -k3,3nr teosinte_chr8_dash.txt > teosinte_snp_chr8_reversed.txt

$ sort -k3,3n maize_chr9.txt > maize_snp_chr9.txt 

$ sort -k3,3n teosinte_chr9.txt > teosinte_snp_chr9.txt

$ sort -k3,3nr maize_chr9_dash.txt > maize_snp_chr9_reversed.txt 

$ sort -k3,3nr teosinte_chr9_dash.txt > teosinte_snp_chr9_reversed.txt

$ sort -k3,3n maize_chr10.txt > maize_snp_chr10.txt 

$ sort -k3,3n teosinte_chr10.txt > teosinte_snp_chr10.txt

$ sort -k3,3nr maize_chr10_dash.txt > maize_snp_chr10_reversed.txt 

$ sort -k3,3nr teosinte_chr10_dash.txt > teosinte_snp_chr10_reversed.txt

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
