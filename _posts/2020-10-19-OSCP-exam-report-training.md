---
layout: post
title: OSCP exam report - training
tags: [OSCP, Cheatsheet, Report, Training]
description: "OSCP exam report - training"
---

# Table of contents

- [Table of contents](#table-of-contents)
- [OSCP EXAM REPORT - TRAINING](#oscp-exam-report---training)
  - [Report templates](#report-templates)
    - [Reports downloading](#reports-downloading)
    - [Requirements](#requirements)
  - [Scripts for report generation](#scripts-for-report-generation)
    - [Generate report script](#generate-report-script)
    - [Submission script](#submission-script)
    - [Make scripts executable](#make-scripts-executable)
  - [Report generation](#report-generation)
  - [Report training](#report-training)
    - [Markdown editor](#markdown-editor)
    - [Markdown cheat sheet](#markdown-cheat-sheet)
    - [Training](#training)
    - [Other](#other)
  - [Tips on report generation](#tips-on-report-generation)
    - [Backslash](#backslash)
    - [Tabulation](#tabulation)
    - [Text color](#text-color)
    - [Code syntax background color](#code-syntax-background-color)
  - [Tips before the exam](#tips-before-the-exam)
    - [Proctoring requirements](#proctoring-requirements)
    - [OSCP Exam Guide](#oscp-exam-guide)
    - [OSCP FAQ](#oscp-faq)

# OSCP EXAM REPORT - TRAINING 

## Report templates

### Reports downloading

Download the templates :

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

For my part I choose **OSCP-exam-report-template_whoisflynn_v3.2.md**, so any training will be done with this one.

### Requirements

You'll need to install a few things :

- [Pandoc](https://pandoc.org/installing.html)
- LaTeX (eg. [TeX Live](http://www.tug.org/texlive/)) in order to get `pdflatex` or `xelatex`
- [Eisvogel Pandoc LaTeX PDF Template](https://github.com/Wandmalfarbe/pandoc-latex-template#installation)
- [p7zip](http://p7zip.sourceforge.net/) (if you want to use the script, for generating the archive)
- [evince](https://wiki.gnome.org/Apps/Evince) (apt install evince)

## Scripts for report generation

### Generate report script

This script is for the report generation in PDF from markdown.

```bash
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
--highlight-style zenburn

if [ $? -eq 0 ]
then
    evince $2
fi
```

### Submission script

This script is to generate the password protected **.7z**, once your report is finish. I commented the LAB_REPORT part of the script because I did not do it.

```bash
# make_submission.sh

#!/bin/bash

OSID="XXXXX"
EXAM_REPORT="OSCP-OS-$OSID-Exam-Report.pdf"
# LAB_REPORT="OSCP-OS-$OSID-Lab-Report.pdf"
ZIP_PACKAGE="OSCP-OS-$OSID-Exam-Report.7z"

echo "Generating exam report..."
./generate_report.sh ../exam/OSCP_exam_report.md $EXAM_REPORT

# echo "Generating lab report..."
# ./generate_report.sh lab_report.md $LAB_REPORT

echo "Creating 7z package..."
# 7z a $ZIP_PACKAGE -pOS-$OSID $EXAM_REPORT $LAB_REPORT
7z a $ZIP_PACKAGE -pOS-$OSID $EXAM_REPORT
```

### Make scripts executable

```bash
chmod +x generate_report.sh make_submission.sh
```

## Report generation

You should have something like that :

![Directory listing](/assets/imgs/report/listing_files.PNG)

Now to test that everything is working let's try to generate a report from markdown.

```
./generate_report.sh OSCP-exam-report-template_whoisflynn_v3.2.md test.pdf
```

Wait a few seconds and a PDF report called **test.pdf** of 9 pages should open.

## Report training 

### Markdown editor

To edit the markdown template, I used [Typora](https://typora.io/).

### Markdown cheat sheet

If you want to know some more about markdown syntax :

- [https://www.markdownguide.org/cheat-sheet/](https://www.markdownguide.org/cheat-sheet/)

### Training

To train myself at reporting, I train on buffer overflow. Why buffer overflow ? Because I knew that at the exam there was one. So if I do it right, during the real exam, I would not have to do much change to my report training.

I did my training on this box :

- [Brainpan](https://tryhackme.com/room/brainpan)

So I took screenshots during the box, they're all inside a directory that I called **images**. Here's what my folder look like : 

![Directory listing](/assets/imgs/report/listing_files_2.PNG)

Here's how I generated it (as in [Report generation](#report-generation)) :

```
./generate_report.sh OSCP-exam-report-template_whoisflynn_v3.2.md test.pdf
```

Here's what my training report looks like :

- Markdown : [https://github.com/Liodeus/liodeus.github.io/blob/master/_posts/OSCP-exam-report-template_whoisflynn_v3.2.md](https://github.com/Liodeus/liodeus.github.io/blob/master/_posts/OSCP-exam-report-template_whoisflynn_v3.2.md)
- PDF : [https://github.com/Liodeus/liodeus.github.io/blob/master/_posts/test.pdf](https://github.com/Liodeus/liodeus.github.io/blob/master/_posts/test.pdf)

But I highly advice that you do it yourself, don't just take mine, practice !

### Other

I just trained reporting on Buffer Overflow but if you want to train your reporting on other box, here's what I found :

- Jeeves (25 Points)
- Chatterbox (20 Points)
- Cronos (20 Points)
- Sense (10 Points)

Here is a report example from Offensive Security :

- [https://www.offensive-security.com/pwk-online/PWK-Example-Report-v1.pdf](https://www.offensive-security.com/pwk-online/PWK-Example-Report-v1.pdf)

## Tips on report generation

### Backslash

If backslashes are in **code** syntax, there is no generation problems.

![Code syntax](/assets/imgs/report/in_code.PNG)

But if you want to print it as **text**, this is a problem. You have to double it, like so :

![Directory listing](/assets/imgs/report/double.PNG)

### Tabulation

To make a tabulation I used the Latex syntax :

```
\quad <TEXT>
```

### Text color

To change the text color, I used the Latex syntax :

```
\textcolor{<COLOR>}{<TEXT>}
```

The predefined color names are

```
black, blue, brown, cyan, darkgray, gray, green, lightgray, lime, magenta, olive, orange, pink, purple, red, teal, violet, white, yellow
```

More infos on Latex colors :

- [https://en.wikibooks.org/wiki/LaTeX/Colors](https://en.wikibooks.org/wiki/LaTeX/Colors)

### Code syntax background color

If you want to change the background color of the code markdown syntax, you just have to change the line 21 of generate_report.sh

```
--highlight-style <STYLE>
```

- kate
- monochrome
- breezeDark
- espresso
- zenburn
- haddock
- tango

You should try them all, to see the one that you like the most.

## Tips before the exam

### Proctoring requirements

Follow this tutorial before your exam to install all requirements concerning the proctoring :

- [https://help.offensive-security.com/hc/en-us/articles/360050299352-Proctoring-Tool-Student-Manual](https://help.offensive-security.com/hc/en-us/articles/360050299352-Proctoring-Tool-Student-Manual)

### OSCP Exam Guide

Read the OSCP Exam Guide :

- [https://help.offensive-security.com/hc/en-us/articles/360040165632](https://help.offensive-security.com/hc/en-us/articles/360040165632)

### OSCP FAQ

Have some questions ? Read the OSCP FAQ :

- [https://help.offensive-security.com/hc/en-us/articles/360050164111-OSCP-Certification-Exam-FAQ](https://help.offensive-security.com/hc/en-us/articles/360050164111-OSCP-Certification-Exam-FAQ)