```
if :; then echo "always true"; fi
if /bin/true; then echo "always true"; fi
if /bin/false; then echo "always true"; fi
if ./a.out; then echo "always true"; fi
```
