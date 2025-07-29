# Building CraftBukkit for Beta 1.7.3

## Bukkit

We need this since it is a dependency.

### Cloning Bukkit

```sh
git clone https://github.com/Bukkit/Bukkit.git
cd Bukkit
git checkout da29e0a
```

### Fixing the `pom.xml`

```sh
sed -i 's,<source>1.5</source>,<source>1.8</source>,g' pom.xml
sed -i 's,<target>1.5</target>,<target>1.8</target>,g' pom.xml
```

### Installing Bukkit

```sh
mvn install
```

## CraftBukkit

### Cloning CraftBukkit

```sh
git clone https://hub.spigotmc.org/stash/scm/spigot/craftbukkit.git
cd craftbukkit
git checkout 59babb2
```

### Fixing the `pom.xml`

```sh
sed -i 's,http://repo.bukkit.org/artifactory/repo,https://raw.githubusercontent.com/canyonmodded/mc-server/main,g' pom.xml
sed -i 's,http://repo.bukkit.org/artifactory/plugins-release,https://repo.papermc.io/repository/maven-public/,g' pom.xml
sed -i 's,<source>1.5</source>,<source>1.8</source>,g' pom.xml
sed -i 's,<target>1.5</target>,<target>1.8</target>,g' pom.xml
```

### Fixing the source code

It won't compile otherwise.

```sh
sed -i 's@converter.convert(name, new ConvertProgressUpdater(console));@try {converter.convert(name, new ConvertProgressUpdater(console));} catch (Exception err) {}@g' src/main/java/org/bukkit/craftbukkit/CraftServer.java
sed -i 's@convertable.convert(s, new ConvertProgressUpdater(this));@try {convertable.convert(s, new ConvertProgressUpdater(this));} catch (Exception err) {}@g' src/main/java/net/minecraft/server/MinecraftServer.java
```

### Compiling CraftBukkit

```sh
mvn package
```