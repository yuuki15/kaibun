# Japanese palindromes

* https://dumps.wikimedia.org/jawiki/latest/jawiki-latest-all-titles-in-ns0.gz
* https://dumps.wikimedia.org/jawiktionary/latest/jawiktionary-latest-all-titles-in-ns0.gz
* https://dumps.wikimedia.org/enwiki/latest/enwiki-latest-all-titles-in-ns0.gz
* https://dumps.wikimedia.org/enwiktionary/latest/enwiktionary-latest-all-titles-in-ns0.gz

```bash
perl -Mutf8 -C -nlE 'length($_)>=3 and /^[ぁ-ゖァ-ヶー]+$/ and /^((.)(?:(?1)|.?)\2)$/ or next; tr/ァ-ヶ/ぁ-ゖ/; $a[length$_]{$_}=1; END { for$i(3..$#a){ %{$a[$i]} or next; open$fh,">",sprintf"%02d.txt",$i; print $fh $_ for sort keys %{$a[$i]}; close$fh } }' *-ns0.txt
```

```bash
perl -Mutf8 -C -nlE 'length($_)>=5 and /[ぁ-ゖァ-ヶー]/ and ($p)=/((.)(?:(?1)|.?)\2)/ and length($p)>=5 and length($p)!=length($_) and $p=~/^[ぁ-ゖァ-ヶー]+$/ or next; $p=~tr/ァ-ヶ/ぁ-ゖ/; $a[length$p]{$p}=$_; END{ open$fh,">","sub.txt"; for$i(3..$#a){ print $fh "$_\t$a[$i]{$_}" for sort keys %{$a[$i]} } close$fh }' *-ns0.txt
```
