#!/usr/bin/env python

# PD the Ripper
# If you thought Jack was mean.....

import os
import color_console as cons
import sys
import glob
from subprocess import check_output
import re

def menume():
    ripper_path = raw_input("Path to regripper: ")
    input_dir = raw_input("Input Directory: ")
    output_dir = raw_input("Output Directory: ")
    host_name = raw_input("Hostname: ")
   # ripper_path = "C:\RegRipper"
   # input_dir = "C:\Users\Hanson\Desktop\uk_uk908851_DGIM_EC"
   # output_dir = "C:\output"
   # host_name="ccc"
    checkthingsexist(ripper_path, input_dir, output_dir, host_name)


def checkthingsexist(ripper_path, input_dir, output_dir, hostname):
    print(os.path.isdir(ripper_path))
    print(os.path.exists(ripper_path + "\\rip.exe"))
    if (os.path.isdir(ripper_path)):
        sucessure("Regripper directory located")
    else:
        failture("Regripper directory not found")
    if os.path.exists(ripper_path + "\\rip.exe"):
        sucessure("Rip.exe located")
    else:
        failture("rip.exe not found in directory" + ripper_path)
    try:
        if os.path.isdir(input_dir):
            sucessure("Input Directory is Valid")
        else:
            failture("Input Directory is Invalid")

    except:
        failture("Something isnt quite right with" + input_dir)
    try:
        if os.path.isdir(output_dir):
            sucessure("Output Directory is Valid")

        else:
            warningsure("Output Directory not found")
            warningsure("We can create that now (y) or return to menu (n)")
            createdir = raw_input("Create Directory: ")
            createdir = createdir.lower()
    except:
        failture("Something not right with " + output_dir)

    if createdir == 'y':
        try:
            if not os.path.exists(output_dir):
                os.makedirs(output_dir)
        except:
            print "Directory Creation Failed"
            menume()
    else:
        failture("You chose not to create directory returning to menu....")
        # os.system('cls')
        menume()
    gsd(input_dir, ripper_path, output_dir, hostname)


def gsd(input_dir, ripper_path, output_dir, hostname):
    os.chdir(input_dir)
    for file in glob.glob("SYSTEM"):
        print file
        outputcommand=("cd " + ripper_path + " && rip.exe -r " + input_dir + "\\" + file + " -f all > " + output_dir + "\\" + hostname + "_SYSTEM_RR.txt")
        print outputcommand
        check_output("" + outputcommand + "", shell=True)
        mastertimeline(file, output_dir, ripper_path, input_dir,hostname)
    i = 0
    for file in glob.glob("*NTUSER.DAT"):
        i += 1
        print file
        j = str(i)
        filetocheck = output_dir + "\\" + hostname + "_" + j + "_ntuser_RR.txt"
        outputcommand = ("cd " + ripper_path + " && rip.exe -r " + input_dir + "\\" + file + " -f ntuser > " + filetocheck)
        print outputcommand
        check_output("" + outputcommand + "", shell=True)
        mastertimeline(file, output_dir, ripper_path, input_dir, hostname)

    for file in glob.glob("SECURITY"):
        outputcommand = ("cd " + ripper_path + " && rip.exe -r " + input_dir + "\\" + file + " -f security > " + output_dir + "\\" + hostname + "_SECURITY_RR.txt")
        print outputcommand
        check_output("" + outputcommand + "", shell=True)
        mastertimeline(file, output_dir, ripper_path, input_dir, hostname)
    for file in glob.glob("SOFTWARE"):
        outputcommand = ("cd " + ripper_path + " && rip.exe -r " + input_dir + "\\" + file + " -f software > " + output_dir + "\\" + hostname + "_SOFTWARE_RR.txt")
        print outputcommand
        check_output("" + outputcommand + "", shell=True)
        mastertimeline(file, output_dir, ripper_path, input_dir, hostname)
    for file in glob.glob("SAM"):
        outputcommand = ("cd " + ripper_path + " && rip.exe -r " + input_dir + "\\" + file + " -f security > " + output_dir + "\\" + hostname + "_SAM_RR.txt")
        print outputcommand
        check_output("" + outputcommand + "", shell=True)
        mastertimeline(file, output_dir, ripper_path, input_dir, hostname)
    for file in glob.glob("amcache.hve"):
        outputcommand = ("cd " + ripper_path + " && rip.exe -r " + input_dir + "\\" + file + " -f security > " + output_dir + "\\" + hostname + "_amcache.txt")
        print outputcommand
        check_output("" + outputcommand + "", shell=True)
        mastertimeline(file, output_dir, ripper_path, input_dir, hostname)
    i = 0
    for file in glob.glob("*usrclass.DAT"):
        i += 1
        print file
        j = str(i)
        filetocheck = output_dir + "\\" + hostname + "_" + j + "_usrclass_RR.txt"
        outputcommand = ("cd " + ripper_path + " && rip.exe -r " + input_dir + "\\" + file + " -f all > " + filetocheck)
        print outputcommand
        check_output("" + outputcommand + "", shell=True)
        mastertimeline(file, output_dir, ripper_path, input_dir, hostname)


def mastertimeline(file, output_dir, ripper_path, input_dir, hostname):
    outputcommand = ("cd " + ripper_path + " && rip.exe -r " + input_dir + "\\" + file + " -p regtime -c > " + output_dir + "\\" + hostname + "_timeline_RR.csv")
    check_output("" + outputcommand + "", shell=True)


def failture(ustats):
    cons.FOREGROUND_RED
    print "[x] Failed: " + ustats
    cons.FOREGROUND_WHITE
    print " Returning to menu......"
    # os.system('cls')
    menume()

def sucessure(ustats):
    cons.FOREGROUND_GREEN
    print "[-] Passed: " + ustats
    cons.FOREGROUND_WHITE

def warningsure(ustats):
    cons.FOREGROUND_YELLOW
    print "[?] Warning: " + ustats
    cons.FOREGROUND_WHITE
    return


if __name__ == "__main__":
    cons.FOREGROUND_WHITE
    print "Version1.0  - Bug in directory creation on windows...output directory needs to exists"
    print "No super timeline yet - will be coming soon"
    menume()

