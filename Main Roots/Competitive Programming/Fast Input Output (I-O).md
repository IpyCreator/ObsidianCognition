---
Label:
  - intermediate
Status: Miscellaneous
---
```Plain
ios_base::sync_with_stdio(false);
cin.tie(NULL);
```

```Plain
void fastscan(int &number) {
    bool negative = false;
    register int c;
    number = 0;
    c = getchar();
    if (c == '-') {
        negative = true;
        c = getchar();
    }
    for (; (c>47 && c<58); c=getchar())
        number = number * 10 + c - 48;
    if (negative)
        number *= -1;
}
```