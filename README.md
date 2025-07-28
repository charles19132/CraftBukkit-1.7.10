# Building CraftBukkit for Minecraft 1.7.10

This tutorial was made due to the sheer amount of errors when compiling 1.7.10-era server software. Now we can finally make clean builds easily again.

## Bukkit

We need this since it is a dependency.

### Cloning Bukkit

```sh
git clone https://github.com/Bukkit/Bukkit.git
cd Bukkit
```

### Fixing the `pom.xml`

This will fix the repos.

```sh
sed -i '25,38d' pom.xml
```

This will fix the JDK version.

```sh
sed -i 's,<source>1.6</source>,<source>1.8</source>,g' pom.xml
sed -i 's,<target>1.6</target>,<target>1.8</target>,g' pom.xml
```

### Installing Bukkit

```sh
mvn install
```

## CraftBukkit

Make sure to `cd ..` after installing Bukkit!

### Cloning CraftBukkit

This will clone an unmodified fork made just before the DMCA takedowns.

```sh
git clone https://github.com/Byteflux/CraftBukkit.git
cd CraftBukkit
```

### Fixing the `pom.xml`

This will remove Overmapped.

```sh
sed -i '324,341d' pom.xml
```

This will fix the repos.

```sh
sed -i '28,37d;41,44d;48,51d' pom.xml
sed -i 's,</repositories>,<repository><id>papermc</id><url>https://repo.papermc.io/repository/maven-public/</url></repository></repositories>,g' pom.xml
```

This will fix the JDK version.

```sh
sed -i 's,<source>1.6</source>,<source>1.8</source>,g' pom.xml
sed -i 's,<target>1.6</target>,<target>1.8</target>,g' pom.xml
```

### Compiling Spigot

```sh
mvn package
```
