Here is a GitHub‑ready README for your NCERT code‑to‑title decoder, including Google Colab hosting steps and a rationale tailored to your iGyan AI workflow needs to translate NCERT filename codes into clear book, subject, and chapter names.​

NCERT Code‑to‑Title Decoder
Decode NCERT chapter PDF codes like lech101 or fsde101 into human‑readable labels such as “Class 12 | English | Chemistry | Part 1, Chapter 01” or “Class 6 | Sanskrit | Sanskrit | Part 1, Chapter 01,” with an optional first‑page PDF text check for extra certainty when needed ​.

Why this exists
NCERT hosts textbooks as chapter PDFs whose filenames embed class, medium, subject, part, and chapter, which is compact but hard to read at a glance for data labeling and ingestion tasks.​

This tool converts those codes into clear titles and can confirm by reading the first page of each PDF, streamlining pipelines such as content tagging, indexing, and automated QA at iGyan AI.​

What it does
Parses NCERT filename codes of the form class letter + medium letter + two‑letter subject + part digit + chapter/suffix into class, medium, subject, part, and chapter fields, e.g., lech101 → Class 12, English, Chemistry, Part 1, Chapter 01.​

Recognizes multiple subjects and mediums used across classes 1–12, including Sanskrit codes like fsde101 for Class 6 Sanskrit chapters and English/Hindi/Urdu counterparts for science and humanities streams.​

Optionally reads the first page text to extract visible headings for robust confirmation of book and chapter titles when encountering unfamiliar codes or special sections like prelims or answers.​

Filename pattern
The general structure is: a single class letter a–l (Classes 1–12) + a medium letter (e/h/u/s) + a two‑letter subject code + a part digit (1 or 2) + a chapter code or suffix (e.g., 01 or an/ps) as seen across NCERT’s Textbooks PDF portal and example links like lech101 and leph105.​

Examples: lech101 (Class 12 Chemistry Part 1 Chapter 01), leph105 (Class 12 Physics Part 1 Chapter 05), lecs103 (Class 12 Computer Science Part 1 Chapter 03), jemh101 (Class 10 Mathematics Part 1 Chapter 01), fsde101 (Class 6 Sanskrit Part 1 Chapter 01), fees1ps (Class 6 Social Science prelims).​

Supported mappings
Mediums: e=English, h=Hindi, u=Urdu, s=Sanskrit, which align to official NCERT language variants present in the Textbooks PDF directory and Sanskrit titles like “वयं वर्णमालां पठामः” in Class 6.​

Subjects: mh=Maths, ph=Physics, ch=Chemistry, bo=Biology, bt=Biotechnology, lm=Lab Manual, sc=Science, ss=Social Science, es=Class 6 Social Science “Exploring Society,” gy=Geography, hs=History, ps=Political Science, ec=Economics, ac=Accountancy, bs=Business Studies, cs=Computer Science, ip=Informatics Practices, py=Psychology, sy=Sociology, he=Home Science, sp=English Supplementary Reader (Snapshots) as confirmed by representative NCERT chapter PDFs and prelims files linked below.​

Live in Google Colab
Open a new Colab notebook, paste the decoder code into a single cell, and run it; Colab environments pass hidden flags to the kernel, so use parse_known_args or a function entry point to avoid the common “unrecognized arguments: -f” error in notebooks.​

The interactive mode can use Python’s input() to decode one code at a time, while the batch mode can read an NCERT ZIP and produce JSON/CSV labels for every chapter PDF in the archive for downstream use.​

Quick start (Colab)
Create a new notebook, install PyPDF2 if you want the first‑page title confirmation step, and run the definitions cell first to register the regex, subject/medium maps, and helper functions in the kernel.​

Use the interactive cell to type codes like lech101, fsde101, or jemh101 and immediately see “Class | Medium | Subject | Part, Chapter ##” labels, which mirror the structure NCERT uses online for chapter PDFs ​.

python
# Optional: PDF title extraction support
!pip install PyPDF2

# Paste the full decoder (regex + MEDIUM_MAP + SUBJECT_MAP + explain/decode_code) in one cell and run it

# Interactive example
# After running the cell that defines 'explain', try:
# explain("lech101")     # → Class 12 | English | Chemistry | Part 1, Chapter 01
# explain("fsde101")     # → Class 6  | Sanskrit | Sanskrit  | Part 1, Chapter 01
# explain("jemh101")     # → Class 10 | English | Mathematics | Part 1, Chapter 01
For batch operation, upload an NCERT ZIP to Colab and call run_zip("/content/NCERT_Textbooks.zip", json_out="index.json", csv_out="index.csv") to generate machine‑readable outputs suitable for search or ingestion at iGyan AI, with the optional first‑page check helping when identifying prelims or answers.​

Local usage
Run the script from a terminal to parse a ZIP or import the module and call run_zip within your Python environment; if running inside a notebook, prefer a function entry point or parse_known_args to avoid IPython’s hidden -f flag causing argparse errors in the kernel.​

The outputs include both a label derived from the filename and, when using PyPDF2, a label derived from the first page (book/chapter headings), letting you decide how to present names in your UI or datastore for iGyan AI tasks.​

Examples
lech101.pdf → “Class 12 | English | Chemistry | Part 1, Chapter 01,” confirming the Chemistry series and class/part encoding in the filename seen on NCERT’s Textbooks portal ​.

leph105.pdf → “Class 12 | English | Physics | Part 1, Chapter 05,” matching the Physics book’s chapter numbering scheme online ​.

lecs103.pdf → “Class 12 | English | Computer Science | Part 1, Chapter 03,” consistent with the Computer Science chapter files published by NCERT ​.

jemh101.pdf → “Class 10 | English | Mathematics | Part 1, Chapter 01,” which aligns with the standard Class 10 Maths chapter layout ​.

fees101.pdf → “Class 6 | English | Social Science | Part 1, Chapter 01,” in the “Exploring Society: India and Beyond” series indicated by the fees prefix ​.

fsde101.pdf → “Class 6 | Sanskrit | Sanskrit | Part 1, Chapter 01,” with the PDF title “वयं वर्णमालां पठामः” confirming language/content ​.

Design notes
The regex accepts any a–z medium letter to remain forward‑compatible, with labeling controlled by MEDIUM_MAP so that Sanskrit s and other mediums decode properly while preserving the established filename structure NCERT uses across its site.​

The optional first‑page text read mirrors visible headings and makes the tool resilient when new subject codes appear or when distinguishing prelims/answers via suffixes like ps/an, which are common in NCERT packaging.​


Known limitations
Some Social Science distributions in Classes 6–10 use umbrella codes (ss/es) while the book branding varies, so prefer enabling the PDF first‑page confirmation step when you need the exact printed title on output assets.​

Prelims and answers are encoded as trailing suffixes (ps/an) and not chapters, so the tool labels them as sections rather than assigning a chapter number to maintain semantic correctness with NCERT’s packaging.​

Contributing
Issues and PRs are welcome for new subject codes, additional mediums, or improved PDF‑title heuristics, keeping alignment with NCERT’s current Textbooks PDF structure and adding examples that validate new mappings.​

​

Acknowledgments
Thanks to NCERT for publicly hosting textbook PDFs that consistently encode class, medium, subject, part, and chapter in filenames, making automated decoding practical for educational data pipelines.​

Example references in this README point to representative PDFs like lech101, leph105, lecs103, jemh101, fees1ps, and fsde101 to illustrate coverage and correctness across streams and languages.​

Appendix: Colab tips
In notebooks, IPython injects flags like -f into argv; use parse_known_args or a callable function entry point to avoid “unrecognized arguments” errors during interactive runs, which is a common pattern for CLI code inside Jupyter/Colab.​

If interactive input seems unresponsive, click into the input prompt area under the cell to ensure focus, which is a known usability nuance in some Jupyter builds during stdin reads with input().
