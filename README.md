# gifrop_examples  






cat Burks.tsv |awk -F '\t' '{print $16}'| awk -F '/' '{print $0 FS $10 "_genomic.fna.gz"}' |sed '1d'
 1054  cat Burks.tsv |awk -F '\t' '{print $16}'| awk -F '/' '{print $0 FS $10 "_genomic.fna.gz"}' |sed '1d' > burks.ftp
 1055  mv burks.ftp burks
 1056  cd burks/
 1057  ls
 1058  cat burks.ftp
 1059  parallel wget {} ::: burks.ftp
 1060  cat burks.ftp | parallel 'wget {}'
 1061  clear

https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5369199/ burks paper
