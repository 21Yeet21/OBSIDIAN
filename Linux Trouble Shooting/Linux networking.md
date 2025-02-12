
## this how i manage to delete all of these bridges in one command :

```bsh
for br in virbr0 virbr1 virbr2 virbr3 virbr4; do
    sudo ip link delete $br
done
```
