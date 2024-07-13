# SIC-XE-Assembler
SIC/XE Assembler with control sections implemented in C++
# Introduction

SIC/XE stands for Simplified Instructional Computer Extra Equipment or Extra Expensive . 
This computer is an advance version of SIC . Both SIC and SIC/XE are closely related to each 
other that’s why are upward compatible .

## Memory :
Memory consists of 8 bit-bytes and the memory size is 1 megabytes (220 bytes). 
Standard SIC memory size is very small. This change in the memory size leads to change in 
the instruction formats as well as addressing modes. 3 consecutive bytes form a word (24 
bits) in SIC/XE architecture. All address are byte addresses and words are addressed by the 
location of their lowest numbered byte.
## Registers : 
It contains 9 registers (5 SIC+ 4 Additional Register ).Four additional registers are : 
1. B : base register 
2. S : General working register 
3. T : General working register 
4. F : Floating point Accumulator 
## Data Formats : 
Integers are represented by binary numbers . Characters are represented 
using ASCII codes . Floating points are represented using 48 bits . 
• Instruction Formats : In SIC/XE architecture there are 4 types of formats available. The Bit(e) 
is used to distinguish between Formats 3 and 4 . e = 0 means Format 3 and e = 1 means 
Format 4 .
• This Assembler also includes Machine – Independent Assembler Features. 
1. Literals 
2. Symbol Defining Statements 
3. Expressions 
4. Control Sections
• The Assembler is implemented our assembler using C++ programming language. 
• The Assembler uses C++ library ifstream to read input from a file and write output on
another file.

# ASSEMBLER DESIGN
## Functions.cpp
-It contains useful functions that will be required by other files .
1) getString: Converts a single character to a string.
2) intToStringHex: Converts an integer to a hexadecimal string with specified fill width.
3) expandString: Expands or truncates a string to a specified length, adding or removing characters 
as necessary.
4) stringHexToInt: Converts a hexadecimal string to an integer.
5) stringToHexString: Converts a string to its hexadecimal representation.
6) checkWhiteSpace: Checks if a character is a white space character.
7) checkCommentLine: Checks if a line is a comment line.
8) if_all_num: Checks if all characters in a string are digits.
9) readFirstNonWhiteSpace: Reads the first non-white space characters from a string.
10) readByteOperand: Reads a byte operand from a string, handling character or hexadecimal byte 
format.
11) writeToFile: Writes data to a file, optionally appending a newline character.
12) getRealOpcode: Extracts the real opcode from a formatted opcode string.
13) getFlagFormat: Determines the flag format of a string.
14) EvaluateString (class): Evaluates arithmetic expressions provided as strings, supporting addition, 
subtraction, multiplication, division, and parentheses.
## Tables.cpp
-It contains all the data structures required for our assembler to run .
1)struct_extdef and struct_extref: These structures represent external definitions and references, 
respectively. They store the name, address, and existence status of external symbols.
2)struct_csect: This structure represents a control section. It holds the name, location counter 
(LOCCTR), section number, length, and tables for external definitions (EXTDEF_TAB) and external 
references (EXTREF_TAB) within the control section.
3)struct_opcode: This structure represents an opcode. It contains the opcode value, format (e.g.,
format 1, format 2, or format 3), and existence status.
4)struct_literal: This structure represents a literal value. It stores the value, address, existence 
status, and block number.
5)struct_label: This structure represents a label. It stores the address, name, relative flag, block 
number, and existence status of a label.
6)struct_blocks: This structure represents a block. It includes the start address, name, location 
counter (LOCCTR), block number, and existence status.
7)struct_register: This structure represents a register. It stores the register number and existence 
status.
8)The code also defines several typedefs for different table types:
SYMBOL_TABLE_TYPE: A map from symbol names to struct_label.
OPCODE_TABLE_TYPE: A map from opcode names to struct_opcode.
REG_TABLE_TYPE: A map from register names to struct_register.
LIT_TABLE_TYPE: A map from literal values to struct_literal.
BLOCK_TABLE_TYPE: A map from block names to struct_blocks.
CSECT_TABLE_TYPE: A map from control section names to struct_csect.
Finally, the functions load_REGTAB(), load_OPTAB(), load_BLOCKS(), and load_tables() initialize the 
opcode table (OPTAB), register table (REGTAB), block table (BLOCKS), and other tables respectively, 
with predefined values.
## Firstpass.cpp
We update the error file and the intermediate file using the source file. If we are unable to 
find the source file, or if the intermediate file doesn’t open, we write the corresponding error 
in the error file; otherwise, we print it to the console. We declare many variables that will be 
required later. Then, the assembler will take the first line as input and check if it is a comment 
line or not. As long as the lines are comments, the assembler prints them to the intermediate 
file and accordingly updates the line number. Once the line is not a comment, we check if 
the opcode is START. If yes, we update the line number, LOCCTR, and start address. If not 
found, we initialize the start address and LOCCTR as 0. Inside the inner loop, we check if the 
line is a comment. If it is a comment, we print it to our intermediate file, update the line 
number, and take in the next input line. If not a comment, we check if there is a label in the 
line. If present, we check if it is present in the SYMTAB. If found, we print an error saying 
‘Duplicate symbol’ in the error file; otherwise, we assign the name, address, and other 
required values to the symbol and store it in the SYMTAB.
Ishaan Jain (22114039)
CSE 2nd Year
## Second.cpp
Assembler takes in the intermediate file as input and generate the intermediate file and the object 
program . Similar to pass1 , if the Assembler is unable to open the file, it will print an error message 
in error file. We then read the first line of the intermediate file. Until the lines are comments, we 
take them as input and print them to our intermediate file and update our line number. If we get 
opcode as ‘START’, we initialize out start address as the LOCCTR, and write the line into the listing 
file. Then we check that whether the number of sections in our intermediate file was greater than 
one, if so, then we update our program length as the length of the first control section or else we 
keep the program length unchanged. For writing the end record we have function . For instructions 
with immediate addressing , we will write the modification record. function_for_reading_till_TAB() : 
takes in the string as input and reads the string until tab(‘\t’) occurs. 
function_for_reading_the_intermediate_file() : Takes in location counter, opcode , operand , label . 
If the line is comment retuns true and takes in the next input line .

# HOW TO RUN(README)
My Enrollment No. is odd and hence, my assembler implements all the required SIC/XE functionalities with 
Control Section. The source code file contains secondpass.cpp, firstpass.cpp, functions.cpp and
tables.cpp.
##  How to Run the Code
1. Extract the sicxe22114039.zip file. (right click on downloaded file and tap extract all.)
2. Open terminal in the sicxe22114039 directory.
3. Compile the code using the command: g++ secondpass.cpp, the compiled program will be written to 
a.exe or a.out depending on the operating system.
4. Run the compiled code using the command: ./a.exe or ./a.out
5. Enter the assembly code file name in the prompt given on running the program.
6. The different results: intermediate, listing, object, tables, errors are written suffixed with the input file 
name.




