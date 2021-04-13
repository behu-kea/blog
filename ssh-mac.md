# Connect to a server using ssh on mac



###  Udfør følgende kommandoer på din lokale computer

```
	$ cd ~
	$ mkdir .ssh
```


### Flyt din *.pem fil fra download mappen til din nye .ssh mappe.    



#### eksempel    

```
	$ pwd
	/Users/clbo/Downloads
	$ mv myFirstKey.pem ../.ssh/myFirstKey.pem
```



### Sørg for at din .pem fil kun har privat read/write adgang.

```
	$ chmod 400 myFirstKey.pem
```



### SSH Connect to server:

```
	$ ssh -i “path-to-pem-file” ec2-user@<public DNS>
```

#### Example:

```
	$ ssh -i "EC2testinstance.pem" ec2-user@ec2-3-15-43-206.us-east-2.compute.amazonaws.com
```

Din <public DNS> finder du i dit EC2 Dashboard.    

Du vil formegentligt se en masse "warnings" når du forbinder. Det er som hovedregel fint og du behøver ikke tage stilling til dem.     

Når du er forbundet vil du se en prompt ala denne:

```
	[ec2-user@ip-172-31-63-172 ~]$
```