---
title: "Remove_middle_element_from_array"
date: 2023-11-02T18:59:18+08:00
draft: false
---

删除数组中间一段
===

```cpp
#include <bits/stdc++.h>
using namespace std;
int main()
{
  int n,d,b;
  cin >> n >> d >> b;
  int c[n];
  for (int i=0;i<n;i++) {
    cin >> c[i];
  } 
  int ju = b-d+1;
  int a[n-ju];
  for (int i=0;i<n;i++) {
    if (i>=d&&i<b) {
      continue;
    } 
    if(i<d) {
      a[i]=c[i];
    }
    if(i>=b) {
      a[i-ju]=c[i];
    }
  }  
  for (int i=0;i<n-ju;i++) {
    cout << a[i] << " ";
  }
}
```