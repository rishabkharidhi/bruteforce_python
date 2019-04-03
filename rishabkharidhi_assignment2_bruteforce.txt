#author : Rishab Kharidhi rishab.kharidhi@colorado.edu
#name   : Assignment 2: Password Cracker Project
#purpose: To perform bruteforce attacks 
#date   : 02.12.2019
#version: 3.7

import sys
import time
import hashlib

#this set of commands are for creating a list of all possible characters from ASCII
alpha=[]
for i in range(65,91):
    alpha.append(chr(i))
for i in range(97,123):
    alpha.append(chr(i))
for i in range(48,58):
    alpha.append(chr(i))
for i in range(33,48):
    alpha.append(chr(i))
for i in range(58,65):
    alpha.append(chr(i))
for i in range(91,97):
    alpha.append(chr(i))
for i in range(123,127):
    alpha.append(chr(i))

count=0
#this function has nested for loops to compute the words for bruteforcing
def bruteforce(inputhash):
    count=0
    for i in alpha:
        #print(i)
        x=i
        hashcheck(x,inputhash)
    for i in alpha:
        for j in alpha:
            x=i+j
            hashcheck(x,inputhash)

    for i in alpha:
        for j in alpha:
            for k in alpha:
                x=i+j+k
                hashcheck(x,inputhash)

    for i in alpha:
        for j in alpha:
            for k in alpha:
                for l in alpha:
                    x=i+j+k+l
                    hashcheck(x,inputhash)

    for i in alpha:
        for j in alpha:
            for k in alpha:
                for l in alpha:
                    for m in alpha:
                        x=i+j+k+l+m
                        hashcheck(x,inputhash)
    for i in alpha:
        for j in alpha:
            for k in alpha:
                for l in alpha:
                    for m in alpha:
                        for n in alpha:
                            x=i+j+k+l+m+n
                            hashcheck(x,inputhash)
    return

#this function is to check if the hash of the word generated is the hash of the password to be cracked
def hashcheck(word,inputhash):
    global count
    whash=hashlib.md5(word.encode())
    wordhash=whash.hexdigest()
    count+=1
    if inputhash == wordhash:
        print("Password cracked\n")
        time2=time.time()
        timetaken=time2-time1
        print("The password is",word)
        print("The password was cracked in "+ str(timetaken) +" seconds")
        print("The number of passwords tried are",str(count))
        sys.exit()
    return

try:
    if __name__=="__main__":
        choice=str(input("Do you want to \n 1) Provide the password as text to be converted to a hash before trying brute-force \n or \n 2) Provide a hash directly for solving\n"))
        if choice=='1':
            #this is to take the input of the word from the user
            inputword=str(input("Enter the word to be cracked / tested\n"))

            inputwhash=hashlib.md5(inputword.encode())
            inputhash=inputwhash.hexdigest()
            time1=time.time()
            bruteforce(inputhash)
                   
        if choice=='2':
            inputhash=str(input("Enter the hash to be cracked / tested\n"))
            time1=time.time()
            bruteforce(inputhash)

        if choice!='1' and choice!='2':
            print("Invalid option choice")
                   
except FileNotFoundError:
    print("The document name that you have entered does not exist, please try again with the proper name")
except ValueError:
    print("The code encountered an error in passing an argument to a function")
except EOFError:
    print("There was an error encountered when taking an input from you. Sorry, please try again!")
##except IOError:
##    print("The code encountered an error when trying to open the file")
except KeyboardInterrupt:
    print("You have over-ridden the processing of this code and cancelled the password cracking operation. Bye!")
except NameError:
    print("You have entered an invalid input, please try again properly!")
#except:
 #   print("Oops sorry, the code ran into some unexpected error!")

