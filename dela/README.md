#Important notes
1. demodela variants run BASE_CLIENTS so they can only download. If you want to move to FULL_CLIENTS, remember to get the HTTP and HTTPS vm forwarded ports in the variables tables. Also remember to get the DELA ports and run the hacky_fix_scripts.

Run all the bellow scenarios from the karamel-chef folder. It currently matters where you are running the scripts from.

# prepare image for hops.site
1. create vagrant image - run from the karamel-chef folder
```
./dela/demodela.sh hopssite
```
2. once the vm is created check the vm ssh port($SSH_PORT) and run 
```
./dela/vm_image_scripts/copy_scripts ${SSH_PORT} hopssite
``` 
3. make sure your image runs this script the first time it boots. Do not run this script as root. Execute as install user(vagrant)
```
/srv/hops/hopssite/image_register.sh
```
4. once successfully execute the above script creates a flag file so that it only executes once per vm - on the very frist bootup. Flag file is: 
```
/srv/hops/hopssite/registered
```
5. step 1 creates/overwrites the cluster definition under cluster-defns/1.demodela.yml

# prepare image for bbc5 mirror
1. create vagrant image - run from the karamel-chef folder
```
./dela/demodela.sh bbc5
```
2. once the vm is created check the vm ssh port($SSH_PORT) type($TYPE - hopssite/bbc5) and run 
```
./dela/vm_image_scripts/copy_scripts ${SSH_PORT} ${TYPE}
``` 
3. make sure your image runs this script the first time it boots. Do not run this script as root. Execute as install user(vagrant)
```
/srv/hops/hopssite/image_register.sh
```
4. once successffuly execute the above script creates a flag file so that it only executes once per vm - on the very frist bootup. Flag file is: 
```
/srv/hops/hopssite/registered
```
5. step 1 creates/overwrites the cluster definition under cluster-defns/1.demodela.yml


# run demodela
Running the cluster-defns/1.demodela.yml requires you to change some of the parameters. 
If you want to run demodela without having to change anything, you can:
1. run with $PARAM - demodela/alex-demodela/hopssite-demodela/bbc5-demodela2 from the karamel-chef folder
```
./dela/demodela.sh $PARAM
```
2. check the cluster file to see the randomly filled variables 
```
cluster-defns/1.demodela.yml
```

# run bbc5 hopssite mirror vm
1. run prepare step 
```
./dela/prepare.sh
```
2. generate vagrantfile and cluster-def 
```
./dela/bbc5_hs_1.sh
```
4. create the vm 
```
./dela/hs_2.sh
```
5. register & install hopssite 
```
./dela/hs_3.sh
```

# run a dev test hopssite vm
1. run prepare step 
```
./dela/prepare.sh
```
2. create env file based on default 
```
dela/defaults/hs_env.sh
```
3. generate vagrantfile and cluster-def 
```
./dela/hs_1.sh ./dela/defauls/hs_env.sh
```
4. create the vm 
```
./dela/hs_2.sh
```
5. register & install hopssite 
```
./dela/hs_3.sh
```

# run dev test dela vm
1. run prepare step 
```
./dela/prepare.sh
```
2. create env file based on default 
```
dela/defaults/dela_env.sh
```
3. generate vagrantfile and cluster-def 
```
./dela/dela_1.sh ./dela/defauls/dela_env.sh
```
4. create the vm 
```
./dela/dela_2.sh
```
