# MAGeT Brain on the CAMH SCC

## Get code

```sh
git clone git@github.com:pipitone/antsRegistration-MAGeT mb
cd mb
git checkout scc
cd ..

git clone git@github.com:pipitone/qbatch
source source.me
```

## Prepare low resolution test set

- get the winterburn HC atlas data

```sh
mb.sh init

for i in WinterburnHippocampalAtlas_MINC/subject*; do 
    autocrop -isostep 10 $i/T1.mnc input/atlas/$(basename $i)_t1.mnc
done

for i in WinterburnHippocampalAtlas_MINC/subject*; do 
    autocrop -noexec -isostep 10 $i/labels.mnc input/atlas/$(basename $i)_label_hc.mnc | \
     sed 's/.*\] //g;s/$/ -keep -near/g' | bash; 
done
```
cp input/atlas/*t1.mnc input/templates/
cp input/atlas/*t1.mnc input/subjects/
```


