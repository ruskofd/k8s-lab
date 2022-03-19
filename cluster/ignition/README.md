### Step 1: prepare cluster virtual machines (Flatcar Linux)

In order to setup Flatcar Linux virtual machines, we need to create an Ignition file and provide it at installation. In my homelab, I use an S3 object storage to store and retrieve Ignition files in my VM once they are booted in live environment.

Firstly, create the **Container Linux Config**, this is the "human-readable" version of the Ignition you will generate :

```YAML
passwd:
  users:
    - name: core
      password_hash: "..."
      ssh_authorized_keys:
        - ssh-ed25519 ...
...
```

Once it's done, you need to transpile it in a specialized JSON file called **Ignition** using the **Config Transpiler** tool called `ct`. Download it [here](https://github.com/flatcar-linux/container-linux-config-transpiler/releases) and then transpile you Config :

```shell
$ ct -in-file k8s.yaml -out-file k8s.ign -pretty
```

In my homelab, I use an S3 object storage server using Minio to make Ignition files accessible for installation (using a bucket allowing anonymous downloads) :

```shell
$ s3cmd put k8s.ign s3://ignition
upload: 'k8s.ign' -> 's3://ignition/k8s.ign'  [1 of 1]
3862 of 3862   100% in    0s   622.36 KB/s  done
```

You can check the file is available :

```shell
$ s3cmd ls s3://ignition
2022-03-19 22:44         3862  s3://ignition/k8s.ign
```

Then, you can start the Flatcar Linux virtual machines using live ISO. You should be directly connected in the virtual machine console and then you can download the Ignition file :

```shell
core@localhost ~ $ wget http://s3.home.lab:9000/ignition/k8s.ign
```

Once it's done, it's possible to launch the installation :

```shell
core@localhost ~ $ sudo flatcar-install -d /dev/sda -i k8s.ign
```

Finally, once the installation is accomplished, reboot the machine, it's ready :)

[Return to main page](../../README.md)
