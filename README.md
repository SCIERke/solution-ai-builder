# solution-ai-builder
solution for ai builder

# Solution-1
```
lst = input() #รับค่า

state_arith = True #check ลำดับเลขคณิต
state_geo = True #check ลำดับเรขาคณิต

d_base = lst[1]-lst[0] # 10 - 5 = 5
i = 1
while (i < len(lst)-1) :
    d = lst[i+1] - lst[i]
    if (d != d_base) :
        state_arith = False
        break
    i += 1

#------------------------------------

r_base  =lst[1] / lst[0]
i = 1
while (i < len(lst) - 1) :
    r = lst[i+1] / lst[i]
    if (r_base != r or r == 0) :
        state_geo = False
        break
    i += 1
if (state_arith) :
    print("Arithmetic")
elif (state_geo) :
    print("Geometric")
else :
    print(-1)
```
