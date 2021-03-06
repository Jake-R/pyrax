# Prax
[Prax](http://www.imdb.com/character/ch0566106/) is a data conversion utility a la radare2's rax. It allows the user to enter a snippet of data in one format and see it in a number of other formats (hex, decimal, binary, raw, Base 64, etc.) and optionally to apply operators to the raw data (swap endianness currently)

# Examples
When no output format is specified, Prax allows you to see all the permutations of the input(s):
~~~~
>> prax 0xdeadbeef
0xdeadbeef 3735928559 Þ­¾ï 3q2+7w==

>> prax -e 0xdeadbeef
0xefbeadde 4022250974 ï¾­Þ 776t3g==

>> prax A@4
0x41424344 1094861636 ABCD QUJDRA==
~~~~

When an output format is specified, then only that format will be printed. using the `-n` flag prints the output without a trailing newline which makes it easy to use prax as input to other programs.
~~~~
>> prax -r 0x41424344
ABCD
>> prax -re 0x41424344
ABCD>>
~~~~
Prax has a built-in parser to evaluate multiple literals according to the following rules:

Rule | Explanation | Example
--- | --- | ---
e1+e2 | concatenate e1 with e2 | `>>prax -r ABCD+0x45464748 -> ABCDEFGH`
e1\*e2 |repeat e1 e2 times | `>>prax -x 0x41*6 -> 0x414141414141`
e1@e2 | repeat e1 e2 times, incrementing by 1 | `>>prax -r 0x30@10 -> 0123456789`
(e1) | evaluate as subexpression | `>>prax -r '(A*4)@5' -> AAAAAAABAAACAAADAAAE`

# Usage
~~~~
>> prax  -h
usage: prax.py [-h] [-n] [-x] [-X] [-d] [-D] [-r] [-R] [-s] [-S] [-b] [-B]
               [-o] [-O] [-e]
               input [input ...]

positional arguments:
  input       literal or expression to parse

optional arguments:
  -h, --help  show this help message and exit
  -n          don't print newline
  -x          output in hex
  -X          force input as hex
  -d          output in decimal
  -D          force input as decimal
  -r          output in ascii
  -R          force input as ascii
  -s          output in Base64
  -S          force input as Base64
  -b          output in binary
  -B          force input as binary
  -o          output in octal
  -O          force input as octal
  -e          Apply "swap endianness" operator to data

~~~~

# Install
~~~~
git clone https://github.com/Jake-R/prax.git
sudo -H pip install -e prax
~~~~

