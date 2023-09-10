#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
@author: ape
"""
import sys
import os
import re
from functools import reduce


# CALL SCRIPT: /home/ape/Scrivania/Programming/Python/latex_anki/latex→anki/parser_latex→anki.py
# os.path.join(sys.argv[2],sys.argv[1])
read_PATH = os.path.join(os.getcwd(),sys.argv[1])
write_PATH = os.path.join(os.getcwd(),sys.argv[1].replace(".tex","_to_be_imported.txt"))

# print(sys.argv[0])
# print(sys.argv[1])

# print(read_PATH)
# print(write_PATH)
## This script takes a tex file with a certain format and produces a .txt file to be imported in anki


fh = open(read_PATH, mode="r", encoding="utf-8")
ls = []

wr = open(write_PATH, mode="w", encoding = "utf-8")
wr.write("#separator:;\n")
wr.write("#notetype column:1\n")

try:
    deck_name = sys.argv[1].replace(".tex","").replace("dmd_","")
    wr.write(f"#deck:{deck_name}\n")
except:
    print("deck name error")
    pass



def clozer(line):
    line = line.replace("\n"," ")
    line = line.split("→")
    line = [ line[0], line[1]+line[2],"clz" ]
    line = ";".join(line)+"\n"
    return line

A = fh.read()
B = re.split(r"(?=\t\t\\item \d*.*?→)",A)[1:-1] #TODO: this is not stable, adding spaces
# can give problems
for elem in B:
    if elem.isspace():
        pass
    try:
     	elem = elem.replace("}}}}","}} }}").replace("}}}","} }}")
    except:
     	pass
    try:
        elem = elem.replace("\n"," ")
        elem = elem.replace("\t\t"+re.findall(r"\\item .*?",elem)[0],"",1)
        elem = elem.split("→")
        try:
            if deck_name!="AM4":
                elem[0] = elem[0]+"."+reduce(lambda x,y: str(ord(y))+x, deck_name,"")
        except:
            pass
        elem[1] = "[latex]"+elem[1]+"[/latex]"
        elem[2] = "[latex]"+elem[2]+"[/latex]"
        
        if "clz" in elem[2]:
            line = ";".join(["Cloze-math"]+elem)+"\n"
            wr.write(line)
        else:
            line = ";".join(["Basic-math"]+elem)+"\n"
            wr.write(line)
    except IndexError:
        print(elem)
        print("→ You might have forgotten a \"→\"")
        pass




 

wr.close()
fh.close()
