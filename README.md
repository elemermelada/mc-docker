# MC Docker
### An OpenGL docker image for the Minecraft client
[![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=fff)](#)

## How to use?
It is most likely that you will have to modify the `CMD` statement in the [Dockerfile](./Dockerfile) to adjust to the specific version of minecraft you want to run. The best way to get the right command is to run Minecraft in the host machine from a working launcher and use the following command:

```bash
ps auxww
```

This will list all running processes (low system activity is thus advised) and it is usually quite easy to spot the one for the Minecraft client, some hints include:
 - It is a `java` or `javaw` binary (depending on the version)
 - The command is usually quite long and includes `net.minecraft.launchwrapper.Launch`

After identifying and copying the launch command, the env vars can be replaced like in the original [Dockerfile](./Dockerfile).

Now the image can be build using [build.sh](./build.sh):

```bash
chmod +x build.sh
./build.sh
```

Finally, to run the image use [run.sh](./run.sh):

```bash
./run.sh <username> <uuid> <accesstoken>
```

Where each argument is replaced with the right value. These values can be obtained from the original launch command, but the token will eventually expire. You can find online [ways to refresh the token](https://kqzz.github.io/mc-bearer-token/).

## Troubleshooting
 - If when running the image there are isues with `iblwjgl.so`, such as "wrong ELF class: ELFCLASS32 (Possible cause: architecture word width mismatch)", replacing `iblwjgl.so` with `iblwjgl64.so` from the same folder might do the trick.
 - You need to make sure you can run GUI apps within docker. There are tons of guides online on how to get this working, a simple ubuntu image running gedit is a good start. If it doesn't work, `mc-docker` will not work.

## Limitations
It is quite obvious from the usage guide that a (preferably ubuntu linux) host machine with a working instalation of Minecraft is needed, so that the configuration can be copied over to the image. 

This image is meant to run Minecraft on a secondary, more restrictive device.

## Why would you need this?
This image enables running a minecraft client in a system where that would not be allowed or advised. Reasons for this include:
 1. Security policies (e.g. _log4j_ is widely used in minecraft and often gets flagged as a vulnerability)
 1. System compatibility (this _may_ solve the "Minecraft runs in my machine" paradigm)
 1. Fun

## Why did I build this?
See No. 1 above.
