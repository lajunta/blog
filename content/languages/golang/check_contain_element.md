---
title: "Check_contain_element"
date: 2023-11-02T11:08:37+08:00
draft: false
---

Check Array Contain Element
===

```go
func contains(array interface{}, val interface{}) (index int) {
    index = -1
    switch reflect.TypeOf(array).Kind() {
    case reflect.Slice:
        {
            s := reflect.ValueOf(array)
            for i := 0; i < s.Len(); i++ {
                if reflect.DeepEqual(val, s.Index(i).Interface()) {
                    index = i
                    return
                }
            }
        }
    }
    return
}
```

