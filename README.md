# solution-ai-builder
solution for ai builder
google colab for 5 , 9 ,11 : [โค้ดสำหรับดูใน google colab ครับ](https://colab.research.google.com/drive/1BUVAevWMlrIrqhcGPMm4QTrchJMRtG-G#scrollTo=PholPew2EjfO)

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
# Solution-2
```
lst = input()
sumd = sum(lst)*2

state = False


for i in range(len(lst)) :
    for j in range(len(lst)):
        if (not(i == j)) :
            if (lst[i]*lst[j] > sumd) :
                state = True
                break

if (state) :
    print("true")
else :
    print("false") 
```
# Solution-3
```
def check(txt) :
    dic = {}
    for i in txt :
        if i in dic :
            dic[i] += 1
        else :
            dic[i] = 1;
    return max(dic.values())

txt = str(input())

lst = txt.split(' ')

lst_check = []

for sub in lst :
    lst_check.append(check(sub))
if (max(lst_check) <= 1) :
  print(-1)
else :
  print(lst[lst_check.index(max(lst_check))])
```
# Solution-4
```
txt = str(input())

lst = []

sum = 0
for i in txt :
    sum += ord(i)
    lst.append(sum)

cnt = 0
state = 1
get = []
for i in range(0,len(lst)) :
    if (cnt) :
        break
    if (lst[i]*2 in lst) :
        get.append(txt[0:i+1])
        state = 0
if (state) :
    print(-1)
else :
    print(get[len(get)-1])
```
# Solution-5
```
import numpy as np
import pandas as pd
import torch

url = 'https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data'
iris_data = np.genfromtxt(url, delimiter=',', dtype=float, usecols=(0, 1, 2, 3))

#print(iris_data)

species = np.genfromtxt(url, delimiter=',', dtype=str, usecols=(4,))
iris_df = pd.DataFrame(iris_data, columns=('sepallength', 'sepalwidth', 'petallength', 'petalwidth'))
iris_df['species'] = species

#print(iris_df)

def get_grouped_mean(data):
    data_group = data.groupby('species').mean()
    return data_group['sepalwidth']

grouped_mean = get_grouped_mean(iris_df)

#print(grouped_mean)

for species, mean in grouped_mean.items():
    print(f"[{species.encode()}, {mean}]")

"""
    ถ้าเธออยากรู้ว่ามันทำงานไง ลองเอาไปรัน google colab แล้วลบ comment พีออกนะคะ
    .groupby(...) --> การรวม data โดย...
    .mean --> หาค่าเฉลี่ยน
    .genfromtxt --> เป็นการดึง data จากไฟล์ text ซึ่งมี parameter เหมาะสม แต่จะได้ เป็นNumPy array.เราจึงต้องจัดการที่หลัง
"""
```
อันนี้ไปดูใน google colab ผม แล้วลองรันได้ครับ
# Solution-6
```
def solve(txt) :
    lst = []
    state = 0
    result = "true"
    for i in txt :
        if (state == 0) :
            if i.isdigit() :
                state += 1
            else :
                state = 0
        else :
            if i.isdigit() :
                if (state == 2) :
                    result = "false"
                    break
                else :
                    state += 1
            else :
                state = 0
    check = []
    for c in txt :
        if c.isdigit() :
            if c in check :
                result = "false"
            else :
                check.append(c)

    return result



txt = input()
lst_txt = txt.split(' ')

result = "true"

for word in lst_txt :
    if (solve(word) == "false") :
        result = "false"
        break

print(result)

"""
    ขั้นตอนแรก เราจากแยก string ออกมาเป็นคำๆ
    จากนั้น เราก็จะ set ค่าแรกเริ่มเอาไว้ state = 0 และเมื่อ state = 2
    มันจะส่งค่า result = "false"
    ซึ่งระบบจะทำงานดังนี้ เมื่อเจอตัวอักษร state จะกลับไปเป็น 0 ทันที
    เมื่อเจอ เลขจะบวกทีละ 1
"""
```
# Solution-7
```
def solve(name) :

    if "password" in name.lower() :
        return "false"
    #cnt_upper = 0 -> 0
    #cnt_number= 0 -> 1
    #cnt_ope = 0 -> 2
    lst_cnt = [0 ,0 ,0]
    for c in name :
        if (c.isupper and c.isalpha()) :
            lst_cnt[0] += 1
        elif ((ord(c) >= 33 and ord(c) <= 47) or (ord(c) >= 58 and ord(c) <= 64) or (ord(c) >= 91 and ord(c) <= 96) or (ord(c) >= 123 and ord(c) <= 126) ) :
            lst_cnt[2] += 1
        elif (c.isdigit()) :
            lst_cnt[1] += 1
    for i in lst_cnt :
        if (i == 0) :
            return "false"
    if len(name) > 7 and len(name) < 31 :
        return "true"
    else :
        return "false"

name = str(input())
print(solve(name))

"""
    นั่นแหละครับ ใช้ ascii แก้ได้หมด
    ord -> แปลง ตัวอักษรให้เป็น ตัวเลข แล้วกำหนดขอบเขตถ้าไปดูในตารางจะรู้เลยว่าเค้าทำอะไร
"""
```
# Solution-8
```
lst = input()

for i in lst :
    sum = 1;
    for j in lst :
        if (i != j) :
            sum *= j
    if (i != lst[len(lst)-1]) :
      print(sum,end="-")
    else :
      print(sum,end="")

"""
  ข้อนี้ทำตามที่มันบอกเลยจ้าง่ายมาก
  อาจจะมีหลอกตรงการ print นิดหน่อย นอกนั้นไม่มีอะไร
"""
```
# Solution-9
ข้อนี้ คือเราไม่แน่ใจว่าเราจัด format ผิดยังไง ลองหาดูนะ
```
import requests
import pandas as pd
from datetime import datetime , timedelta
import json

response = requests.get("https://coderbyte.com/api/challenges/json/date-list")
date_list = eval(response.content.decode('utf-8'))

date_list = sorted(date_list, key=lambda x: x['date'])


real_date = []
date_list_dates = [entry['date'][:10] for entry in date_list]

for i in range(len(date_list)):
    start_str = date_list[i]['date']
    value = date_list[i]['value']
    start = datetime.fromisoformat(start_str.replace('Z', '+00:00'))
    
    if i == 0:
        real_date.append([start_str, value])
    else:
        end_str = date_list[i - 1]['date']
        end = datetime.fromisoformat(end_str.replace('Z', '+00:00'))
        
        if (start - end).days == 0:
            real_date.append([start_str, value])
        else:
            x = pd.date_range(start=end_str[:10], end=start_str[:10], freq='D')
            for j in range(1, len(x)):
              if x[j].strftime('%Y-%m-%d') == start_str[:10] or x[j].strftime('%Y-%m-%d') == end_str[:10] :
                  real_date.append([start_str, value])
              else : 
                real_date.append([x[j].strftime('%Y-%m-%dT%H:%M:%S.%f')[:-3] + 'Z', 0])

json_data = [{"date": date, "value": value} for date, value in real_date]

print(json.dumps(json_data))
```
# Solution-10
```
def update_shopping_cart(cart, action):
    product_id = action.get("product_id")

    if action["type"] == "add":
        if product_id in cart:
            cart[product_id] += action["quantity"]
        else:
            cart[product_id] = action["quantity"]
    elif action["type"] == "remove":
        cart[product_id].pop(product_id)
    elif action["type"] == "change" and action.get("quantity", 0) > 0:
        cart[product_id] = action["quantity"]

    return cart

# do not modify the values below
print(update_shopping_cart({ "product_A": 4, "product_B": 3, "product_C": 1 }, { "type": "change", "product_id": "product_B", "quantity": 2 }))

"""
    ข้อนี้ไม่มีไรมาก อ่านแล้วแก้ตามที่เขาบอก
"""
```
# Solution-11
```
import numpy as np
import requests
import pandas as pd
import json

response = requests.get("https://coderbyte.com/api/challenges/logs/user-info-csv")
csv_as_text = response.content.decode('utf-8')

data = pd.DataFrame([x.split(',') for x in csv_as_text.split('\n')], columns=['Name', 'Email', 'Phone'])
data = data.drop(data.index[0])
data = data.sort_values(by=data.columns[1])
json_data = data.to_json(orient='records')

print(json_data)
```
# Solution-12
```
from itertools import permutations

target = str(input())

use = [i for i in target]

perm = permutations(use)
nume = set()
for i in list(perm):
    number = "".join(i)
    if number not in nume:
        nume.add(int(number))

nume = sorted(nume)
print(nume)
for i in range(len(nume)) :
    if nume[i] == int(target) :
        print(nume[i+1])
        break

"""
    หลักการของข้อนี้คือ ใช้ library ที่เขาให้มา หา permutation จะได้งี้(1, 2, 3)
    (1, 3, 2)
    (2, 1, 3)
    (2, 3, 1)
    (3, 1, 2)
    (3, 2, 1)
    จากนั้นแปลงเจ้าพวกนี้เป็น เลข แล้ว sort ได้งี้ : [123, 132, 213, 231, 312, 321]
    จากนั้น หาตัวที่ต้องการ ได้เลย จบ ซึ่งเขาบอกว่า สูงกว่า 1 ตัว ดังนั้นเราก็หาตัวที่เขาให้มา
    แล้ว + index ไป อีก 1 ก็เลยเป็น i+1

"""
```
