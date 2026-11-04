# Linux cheatsheet

## Rank values in a log
Filter, pick a column, sort, count, then rank:

    grep 500 access.log | awk '{print $1}' | sort | uniq -c | sort -nr

## Find what is using a file
    lsof <file>

## Stop a process
    kill <PID>
