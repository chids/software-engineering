```
$ awk '{print $0}' file #  Print the all column.
$ awk '{print $3}' file #  Print the 3rd column.
$ awk '{print $1 $3}' file #  Print the 1st and the 3rd columns.
```

`tee` to print stdout and log to file.
```
cmd xxx | tee file
```

```
2>&1 # redirect stderr to stdout
>/dev/null 2>&1 # and redirect to black hole
```
### Sum
```
cat numbers.log | python -c "import sys; print sum(int(l) for l in sys.stdin)"
cat numbers.log | ruby -e 'puts STDIN.read.split("\n").map(&:to_i).reduce(:+)'
cat numbers.log | paste -s -d+ infile | bc
```