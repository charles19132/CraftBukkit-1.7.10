# Building Paper for Minecraft 1.7

## Cloning Paper

```sh
git clone https://github.com/PaperMC/Paper-1.7.git
cd Paper-1.7
```

## Cloning submodules

```sh
git submodule init
git submodule update
```

## Applying patches

```sh
./applyPatches.sh
```

## Fixing the `pom.xml` files

```sh
sed -i '25,38d' Bukkit/pom.xml
sed -i '28,37d;41,44d;48,51d;324,341d' CraftBukkit/pom.xml
sed -i 's,</repositories>,<repository><id>papermc</id><url>https://repo.papermc.io/repository/maven-public/</url></repository></repositories>,g' CraftBukkit/pom.xml MinecraftServer/pom.xml
sed -i '20,23d' MinecraftServer/pom.xml
sed -i '29,32d;36,39d;288,305d' PaperSpigot-Server/pom.xml
sed -i 's,<source>1.6</source>,<source>1.8</source>,g' */pom.xml pom.xml
sed -i 's,<target>1.6</target>,<target>1.8</target>,g' */pom.xml pom.xml
```

## Compiling Paper

```sh
mvn package
```