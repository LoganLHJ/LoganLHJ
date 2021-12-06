1.japonicus vcf file에서 '\t' 기준으로 읽어, genomic position 정보와 missense variant region 정보를 불러옴.
import pandas as pd

japonicus_vcf_file = '/BiO/Research/Project2/Japonicus/Analysis/Z.japonicus.filtered_DP5SNV_modified.annot.vcf'
output = '/BiO/Research/Project2/Japonicus/Analysis/01_japonicus_genomic_position_and_missense_variant_region.vcf'

with open(japonicus_vcf_file, 'r') as fr:
    lines_1 = [line.rstrip('\n').split('\t') for line in fr]
df_missense_variant = pd.DataFrame(lines_1)
    
df_missense_variant = df_missense_variant.iloc[:,[0,1,7]]

df_missense_variant.to_csv(output, index=False, sep='\t', header=None)



2.01_japonicus_genomic_position_and_missense_variant_region.vcf에서 '|' 기준으로 읽어, genomic position 정보와 missense variant region 정보를 불러옴.
import pandas as pd
import numpy as np

japonicus_vcf_file = '/BiO/Research/Project2/Japonicus/Analysis/01_japonicus_genomic_position_and_missense_variant_region.vcf'
output = '/BiO/Research/Project2/Japonicus/Analysis/02_japonicus_genomic_position_and_missense_variant_region.vcf'

with open(japonicus_vcf_file, 'r') as fr:
    lines_1 = [line.rstrip('\n').split('|') for line in fr]
df_missense_variant = pd.DataFrame(lines_1)

df_missense_variant = df_missense_variant[df_missense_variant[1]=='missense_variant']

df_missense_variant = df_missense_variant.iloc[:,[0,1,10]]

df_missense_variant.to_csv(output, index=False, sep='\t', header=None)



3-1.02_japonicus_genomic_position_and_missense_variant_region.py에서 '\t' 기준으로 읽어, genomic position 정보와 missense variant region 정보를 불러옴.
3-2.amino acids 3 letters to 1 letter 으로 변경

import pandas as pd

japonicus_vcf_file = '/BiO/Research/Project2/Japonicus/Analysis/02_japonicus_genomic_position_and_missense_variant_region.vcf'
extract_chromosome_position_and_missense_variant = '/BiO/Research/Project2/Japonicus/Analysis/03_japonicus_genomic_position_and_missense_variant_region.vcf'

with open(japonicus_vcf_file, 'r') as fr:
    lines_1 = [line.rstrip('\n').split('\t') for line in fr]
df_missense_variant = pd.DataFrame(lines_1)

df_missense_variant = df_missense_variant.iloc[:,[0,1,3,4]]

df_missense_variant[4] = df_missense_variant[4].str.replace('Val','V').str.replace('Ala','A').str.replace('Asp','D').str.replace('Glu','E').str.replace('Gly','G').str.replace('Phe','F').str.replace('Leu','L').str.replace('Ser','S').str.replace('Tyr','Y').str.replace('Cys','C').str.replace('Trp','W').str.replace('Pro','P').str.replace('His','H').str.replace('Gln','Q').str.replace('Arg','R').str.replace('Ile','I').str.replace('Met','M').str.replace('Thr','T').str.replace('Asn','N').str.replace('Lys','K').str.replace('p.','')

df_missense_variant.to_csv(extract_chromosome_position_and_missense_variant, index=False, sep='\t', header=None)



4.큰따옴표("") 제거
import pandas as pd

japonicus_vcf_file = '/BiO/Research/Project2/Japonicus/Analysis/03_japonicus_genomic_position_and_missense_variant_region.vcf'
extract_chromosome_position_and_missense_variant = '/BiO/Research/Project2/Japonicus/Analysis/extract_chromosome_position_and_missense_variant.vcf'

df_missense_variant= pd.read_csv(japonicus_vcf_file, sep="\s+", header=None)
df_missense_variant[0] = df_missense_variant[0].str.strip("\"")

df_missense_variant.to_csv(extract_chromosome_position_and_missense_variant, index=False, sep='\t', header=None)
