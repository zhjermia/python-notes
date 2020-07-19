## My take and other notes on pythonchallenge.com

### Challenge 1
This challenge is easy. We can directly type into python console 2\*\*38, and replace the internet address page 0, with the result of 2\*\*38 from the console.

### Challenge 2
This one is quite complicated for beginner like me. When I started working on this, it took me a while - I think about two days, with many breaks. 
The clue is `k->m, o->q, e->g`. 
The challenge is to decode this sentence: 
`g fmnc wms bgblr rpylqjyrc gr zw fylb. rfyrq ufyr amknsrcpq ypc dmp. bmgle gr gl zw fylb gq glcddgagclr ylb rfyr'q ufw rfgq rcvr gq qm jmle. sqgle qrpgle.kyicrpylq() gq pcamkkclbcb. lmu ynnjw ml rfc spj.`

So it is obvious from the clue that we should shift each character by two characters down the alphabet (automatically using code).

Here is my solution in python console (I tried using function, but revert back to console as I tried the result of each line to learn).
```
[1] alphabet = 'abcdefghijklmnopqrstuvwxyz'                     #initial definition of alphabet to use in the dictionary
[2] alphabetDict = {alphabet[0]:alphabet[2]}                    #I initiate a dictionary for conversion of each character. This initiation is direct because from the clue I knew that the shifting is two characters.
[3] for i in range(0,26):
...     alphabetDict.update({alphabet[i]:alphabet[(i+2)%26]})   #Here I update the dictionary to complete keys for all alphabet
[4] alphabetDict.update({'.':'.'})                           https://stackoverflow.com/questions/3031045/how-come-string-maketrans-does-not-work-in-python-3-1   #important to update dictionary with each character in the challenge, this line is repeated for other character.
[5] textInput = '`g fmnc wms bgblr rpylqjyrc gr zw fylb. rfyrq ufyr amknsrcpq ypc dmp. bmgle gr gl zw fylb gq glcddgagclr ylb rfyr\'q ufw rfgq rcvr gq qm jmle. sqgle qrpgle.kyicrpylq() gq pcamkkclbcb. lmu ynnjw ml rfc spj.`
#Here I put the challenge into a variable named textInput
[6] textInput_list = list(textInput)                            #I made a list variable for the characters in textInput so later I can use the dictionary to replace the content of this list.
                                                                #Note that I learn from this exercise that we can't replace direcly each character in a string variable.
[7] for i in range(0,len(textInput)):
...    textInput_list[i]=alphabetDict[textInput_list[i]]
                                                                #looping through the textInput_list and replace each character according to the dictionary
... textOutput="".join(textInput_list)                          #re-join the list into string
[8] print(textOutput)                                           #will display the conversion result.
```
Now from the answer, I was suggested to use string.maketrans(). ~~I'm not sure what this is. So I will find out and update this with a solution using that method.~~

After some quick google, I found out that string.maketrans() is deprecated in python 3.x, and replaced by str.makestrans(). A clear example is in here: https://www.tutorialspoint.com/python3/string_maketrans.htm

Another good things is that the characters that are not to be translated will be left intact in the input string.

So with this method, it is much simpler as the following.

```
[1] intab = 'abcdefghijklmnopqrstuvwxyz'
[2] outtab = 'cdefghijklmnopqrstuvwzyzab'         #in this case, to think to use any function is ridiculous, I just typed it manually
[3] trantab = textInput.maketrans(intab,outtab)
[4] textInput = 'g fmnc wms bgblr rpylqjyrc gr zw fylb. rfyrq ufyr amknsrcpq ypc dmp. bmgle gr gl zw fylb gq glcddgagclr ylb rfyr\'q ufw rfgq rcvr gq qm jmle. sqgle qrpgle.kyicrpylq() gq pcamkkclbcb. lmu ynnjw ml rfc spj.'
[5] textOutput = textInput.translate(trantab)
[6] textOutput
```

### Challenge 3
This one is already difficult, but search engines are your friends. So to quote the challenge, here is the clue `recognize the characters. maybe they are in the book,
but MAYBE they are in the page source.
`
The clue is easy: it is to open the html source. In the source, there is a large body of text which seems to be containing random characters. The challenge is to understand what to do with this large body of text. I don't see any other clue, just to "recognize the characters". Hmm, what to do...
Update: after opening the page source, we can find that in the beginning of the <html> tag, there is another clue: `find rare characters in the mess below:`, then the random characters.
