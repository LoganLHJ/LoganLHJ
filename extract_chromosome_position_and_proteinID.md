1.GCF_004028035.1_ASM402803v1_genomic_modified.gff에서 ';' 기준으로 읽어, genomic position 정보와 ProteinID 정보를 불러옴.

import pandas as pd

japonicus_reference_gff_file = '/BiO/Research/Project2/Japonicus/Analysis/GCF_004028035.1_ASM402803v1_genomic_modified.gff'
output = '/BiO/Research/Project2/Japonicus/Analysis/01_japonicus_genomic_position_and_ProteinID.gff'

with open(japonicus_reference_gff_file, 'r') as fr:
    lines_1 = [line.rstrip('\n').split(';') for line in fr]
df_japonicus_reference = pd.DataFrame(lines_1)

df_japonicus_reference = df_japonicus_reference.iloc[:,[0]]

df_japonicus_reference.to_csv(output, index=False, sep='\t', header=None)




2-1.01_japonicus_genomic_position_and_ProteinID.gff에서 '\t' 기준으로 읽어, genomic position 정보와 ProteinID 정보를 불러옴.
2-2.XP_, NP_ (Protein ID 정보 앞)를 포함한 행만 추출
2-3.(Protein ID 정보 앞) 'ID=cds-' 문자열 제거

import pandas as pd

japonicus_reference_gff_file = '/BiO/Research/Project2/Japonicus/Analysis/01_japonicus_genomic_position_and_ProteinID.gff'
output = '/BiO/Research/Project2/Japonicus/Analysis/extract_chromosome_position_and_proteinID.gff'

with open(japonicus_reference_gff_file, 'r') as fr:
    lines_1 = [line.rstrip('\n').split('\t') for line in fr]
df_japonicus_reference = pd.DataFrame(lines_1)

df_japonicus_reference = df_japonicus_reference.iloc[:,[0,3,4,8]]

df_japonicus_reference = df_japonicus_reference[df_japonicus_reference[8].notnull()][df_japonicus_reference[8].dropna().str.contains('XP_|NP_')]

df_japonicus_reference[8]=df_japonicus_reference[8].str.replace('ID=cds-','')

df_japonicus_reference.to_csv(output, index=False, sep='\t', header=None)
