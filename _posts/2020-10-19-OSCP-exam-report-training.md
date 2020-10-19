---
layout: post
title: OSCP exam report - training
tags: [OSCP, Cheatsheet, Report, Training]
description: "OSCP exam report - training"
---

# OSCP EXAM REPORT - TRAINING 

## Report templates

Downloads the templates :

```
git clone https://github.com/noraj/OSCP-Exam-Report-Template-Markdown.git
mkdir report_training
cd OSCP-Exam-Report-Template-Markdown
mv src/OSCP-exam-report-template_* ../report_training/
```

In this repository there is two exam templates :

- OSCP-exam-report-template_whoisflynn_v3.2.md
- OSCP-exam-report-template_OS_v1.md

Choose the one that you prefer between these two, you can see what they'll look like once in PDF format here :

- [OSCP-exam-report-template_whoisflynn_v3.2.pdf](https://github.com/noraj/OSCP-Exam-Report-Template-Markdown/blob/master/output/OSCP-exam-report-template_whoisflynn_v3.2.pdf)
- [OSCP-exam-report-template_OS_v1.pdf](https://github.com/noraj/OSCP-Exam-Report-Template-Markdown/blob/master/output/OSCP-exam-report-template_OS_v1.pdf)

If you don't like any of them here's some more templates from Offensive Security :

- [Microsoft Word](https://www.offensive-security.com/pwk-online/PWKv1-REPORT.doc)
- [OpenOffice/LibreOffice](https://www.offensive-security.com/pwk-online/PWKv1-REPORT.odt)

## Report training 





## Scripts for report generation





## Report generation





## Tips on report generation


```

```



download the latest .deb

```
https://github.com/jgm/pandoc/releases
```

```
wget https://github.com/jgm/pandoc/releases/download/2.10.1/pandoc-2.10.1-1-amd64.deb
```

```
sudo dpkg -i pandoc-2.10.1-1-amd64.deb
```



```
sudo apt install evince
```



Download the latest version of Eisvogel

```
https://github.com/Wandmalfarbe/pandoc-latex-template/releases
```

```
mkdir temp
cd temp
wget https://github.com/Wandmalfarbe/pandoc-latex-template/releases/download/v1.5.0/Eisvogel-1.5.0.zip
mv eisvogel.tex eisvogel.latex
mv eisvogel.latex ../report/
mkdir /usr/share/pandoc/
mkdir /usr/share/pandoc/templates/
mkdir /usr/share/pandoc/data/
mkdir /usr/share/pandoc/data/templates/
cp eisvogel.latex /usr/share/pandoc/templates/
```

```
sudo apt-get install texlive-full
```



```
chmod +x generate_report.sh make_submission.sh
```



```
# generate_report.sh

#!/bin/bash

if [ "$#" -ne 2 ]; then
    echo "usage: $0 <input.md> <output.pdf>"
    exit
fi

# if this machine does not have the template in place, put it there!
if [ ! -e /usr/share/pandoc/data/templates/eisvogel.latex ]
then
    sudo cp eisvogel.latex /usr/share/pandoc/data/templates/
fi

pandoc $1 -o $2 \
--from markdown+yaml_metadata_block+raw_html \
--template eisvogel \
--table-of-contents \
--toc-depth 6 \
--number-sections \
--top-level-division=chapter \
--highlight-style tango

if [ $? -eq 0 ]
then
    evince $2
fi
```



```
# make_submission.sh

#!/bin/bash

OSID="XXXXX"
EXAM_REPORT="OSCP-OS-$OSID-Exam-Report.pdf"
#LAB_REPORT="OSCP-OS-$OSID-Lab-Report.pdf"
ZIP_PACKAGE="OSCP-OS-$OSID-Exam-Report.7z"

echo "Generating exam report..."
./generate_report.sh ../exam/OSCP_exam_report.md $EXAM_REPORT

#echo "Generating lab report..."
#./generate_report.sh lab_report.md $LAB_REPORT

echo "Creating 7z package..."
#7z a $ZIP_PACKAGE -pOS-$OSID $EXAM_REPORT $LAB_REPORT
7z a $ZIP_PACKAGE -pOS-$OSID $EXAM_REPORT
```

