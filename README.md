## Text Tracker
### Background: Running Records
Research shows that one of the best ways to promote literacy in elementary aged
students is to track their progress via the Running Records program, in which
the teacher scores the student's reading abilities in a live, in-person reading
test. This way, teachers can help students in the areas they need most.
However, this process is extremely time consuming, so a small team of students
at Clemson University is researching ways to automate the scoring process.
### Following Along
The two primary challenges of the project are transcribing the student's words,
and keeping track of where the student is in the testing book so that the
transcription may be accurately scored. The transcription part is handled by
third party services such as IBM's Watson, but we were unable to find
pre-existing algorithms that could accomplish the second part: following along
with the student.
### Applications
This package includes tools to analyze text files and align two texts with each
other so that they may be compared or scored. This addresses the problem of
following along with a student during a Running Records assessment.
Applications may extend to any unlimited number of projects, such as plagiarism
detection, soft string matching, and more.
### Usage
This package is available on PyPI and can be installed via

`pip install text-tracker`

and used via
```python
import text_tracker
text_tracker.track([original_file], [spoken_file])
```
or
```python
from text_tracker import track
track([original_file], [spoken_file])
```

View this project on GitHub:

<https://github.com/supercooper6558/Text-Tracker>
### Detailed Operation
Let's say we have two text files with the following content.

File 1:
```
The other day I went to the other store where the day was long
one day a bird met a hippo

```
File 2:
```
The other other day word I i went to the the word the other store the day was long
one day a bird a word bird met a hippo

```
Note that the last line of each file is an empty blank line. _This is
important._

To use the package in python, open both files and pass them to the `track`
function, such as follows:
```python
from text_tracker import track
with open('original.txt', 'r') as o:
    with open('test.txt', 'r') as t:
        indeces = track(o, t)
```
`indeces` would be a list of the following two index vectors:
```python
[0, 1, 1, 2, nan, 3, 3, 4, 5, 6, nan, 6, 6, 7, 8, 10, 11, 12, 13]
[0, 1, 2, 3, 2, nan, 3, 4, 5, 6]
```
What's going on here? The files contain two texts that are being compared.
Capitalization doesn't matter - the algorithm converts everything to lowercase
before doing anything else. The files should contain no punctuation, unless
you want it considered part of a word. The only delimiters is the space
character, so if you have a comma at the end of a word, the program will treat
the comma character as part of the word and likely not find any matches for
that combination. Each line is evaluated separately, so it would be helpful to
use each line as a page in a book. Both files must have the same number of
lines.

The output is a list of index vectors. For each "page" (or line), there is an
associated index vector, where each element maps a spoken word to a written
word. If a word appears in the "spoken" file that does not appear in the
"written" file, it will be associated with NaN.
### Credits
This was developed by Cooper Sanders in 2020 and is MIT licensed. You can
contact me at

<mailto:tromboneguy@coopersanders.com>

clemson.edu domain email addresses can contact me at 

<mailto:cssande@clemson.edu>

My website:

<https://coopersanders.com>