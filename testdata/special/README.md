## special judge ##

原則上跟 strict 很像，只差一個 `special` 檔案

### judge ###

下面是一個範例，同時把 0.in 的內容寫在 0.out 中，讓 special.py 讀入輸入測資，也可以多開一個檔案來完成這件事情 (testdata input `sys.argv[1]`)。

```
#!/usr/bin/env python3
import sys
# 
def rstrip(s):
	while s and (s[-1] == '\r' or s[-1] == '\n'): s = s[:-1]
	return s
# Judge Environment Ubuntu
fa, fb = open(sys.argv[3]), open(sys.argv[2])

try:
	# User Ouput
	fa_lines = fa.readlines()
	user_answer, = (int(val) for val in fa_lines[0].split())

	# Testdata read xxx.out
	fb_lines = fb.readlines()
	n, = (int(val) for val in fb_lines[0].split())
	A = [int(val) for val in fb_lines[1].split()]

	# Compare
	numDict = {}
	for elem in A:
		if elem not in numDict:
			numDict[elem] = 0
		numDict[elem] += 1

	if user_answer not in numDict or numDict[user_answer] < 2:
		quit(1); # Wrong Answer
except:
	quit(1); # Wrong Answer
```