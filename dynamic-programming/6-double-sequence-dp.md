# 匹配类动态规划

  


匹配两个字符串的最优值/方案数/可行性



• state: f\[i\]\[j\]代表了第一个sequence的前i个数字/字符，配上第二个sequence的前j个...

• function: f\[i\]\[j\] = 研究第i个和第j个的匹配关系\(实际上只需研究“上”，“左”，“左上”三个状态\)

• initialization: f\[i\]\[0\] 和 f\[0\]\[i\]

• answer: f\[n\]\[m\] min/max/数目/存在关系

• n = s1.length\(\)

• m = s2.length\(\)

解题技巧画矩阵，填写矩阵

