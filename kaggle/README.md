Step1: 
```
pip install
```

Step2: Export kaggle api vars
```
export KAGGLE_USERNAME=datadinosaur
export KAGGLE_KEY=xxxxxxxxxxxxxx
```

Step3: Download datasets
```
kaggle datasets download -d unitednations/international-greenhouse-gas-emissions
```

Step4: Extract Data
```
unzip international-greenhouse-gas-emissions.zip
```

Step4: CSV -> JSON using Bash Script

sed -ne "${start},${end}p" yourfile
awk "NR >= 1 && NR <= $end" yourfile
perl -ne "print if $start .. $end;" yourfile

https://jqplay.org/s/udzeqTCVFM
https://jqplay.org/s/hgsVv1TY8T

Lint
https://jsonlint.com/

Reference:
http://kb.ictbanking.net/article.php?id=655

```
#by country
awk "NR>=2" <*.csv| jq --raw-input --slurp --raw-output 'split("\n") | .[0:] | map(split(",")) | map(select(.[0]) | { "country": .[0], "year": .[1], "value": .[2], "category": .[3] })' | jq --raw-output 'group_by(.country)[] | { (.[0].country) : ((map({"country", "year", "value", "category" }) )) }' | jq -s add > formatted/dataCountry.json

#by year
awk "NR>=2" <*.csv| jq --raw-input --slurp --raw-output 'split("\n") | .[0:] | map(split(",")) | map(select(.[0]) | { "country": .[0], "year": .[1], "value": .[2], "category": .[3] })' | jq --raw-output 'group_by(.year)[] | { (.[0].year) : ((map({"country", "year", "value", "category" }) )) }' | jq -s add  > formatted/dataYear.json


```

mv * ../../frontend/src/assets/