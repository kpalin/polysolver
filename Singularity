BootStrap:docker
From: sachet/polysolver:v4
%files
     shell_call_hla_type.modern /home/polysolver/scripts/shell_call_hla_type.robust

%post
     mkdir -p /data/input/
     mkdir -p /data/output/
     ln -s /home/polysolver /usr/local/libexec/polysolver
     ln -s /home/samtools /usr/local/libexec/samtools
     export PSHOME=/usr/local/libexec/polysolver
     export SAMTOOLS_DIR=/usr/local/libexec/samtools
     export JAVA_DIR=/usr/bin
     export NOVOALIGN_DIR=$PSHOME/binaries

     # IMPORTANT: the below aren't set, I'm not sure where they are inside image
     export GATK_DIR=$PSHOME
     export MUTECT_DIR=$PSHOME
     export STRELKA_DIR=$PSHOME
     export LC_ALL=C
     unset LANG
     unset LANGUAGE
     for F in $(find /usr/local/libexec/polysolver/scripts/ -type f)
     do
          sed -i 's/\bTMP_DIR=[[:alnum:]_\/.$-]*//' ${F}
     done

     #Writiable tmp directory
     export _JAVA_OPTIONS=-Djava.io.tmpdir=/data/output/
     export TMPDIR=/data/output/
     export TMP_DIR=/data/output/ 
     NOW=`date`
     echo "export NOW=\"${NOW}\"" >> $APPTAINER_ENVIRONMENT
     chmod 777 -R /usr/local/libexec

%environment
     export _JAVA_OPTIONS=-Djava.io.tmpdir=/data/output/ 
     export TMPDIR=/data/output/ 
     export TMP_DIR=/data/output/ 
     export LC_ALL=C
     export PSHOME=/usr/local/libexec/polysolver
     export SAMTOOLS_DIR=/usr/local/libexec/samtools
     export JAVA_DIR=/usr/bin
     export NOVOALIGN_DIR=$PSHOME/binaries
     export GATK_DIR=$PSHOME
     export MUTECT_DIR=$PSHOME
     export STRELKA_DIR=$PSHOME     
     
     
%runscript
    echo "Container was created $NOW"
    echo "Arguments received: $@"
    echo "Expecting data in /data/input/ and /data/output/ "
    exec /bin/bash -euo pipefail    /usr/local/libexec/polysolver/scripts/shell_call_hla_type.robust "$@"