# mahjong-tree-search

A tool to calculate winning probabilities for one-player mahjong.

[Read this in Japanese (日本語).](README.ja.md)

## Usage

### Preparation

- Install CMake.
- Prepare a compiler that supports C++17 or higher.

### Build
- Debug mode
```shell
$ mkdir build
$ cmake .. -DCMAKE_BUILD_TYPE=Debug
$ make
```

- Release mode
```shell
$ mkdir build
$ cmake .. -DCMAKE_BUILD_TYPE=Release
$ make
```

### Calculate
1. Execute the program according to the number of tiles and the calculation method.
2. Enter the hand tiles in "MPSZ" format.
3. Enter the maximum number of drawing.
4. The results are output as a table. The "Prb" column is the winning probability, the "Rdy" column is the "tempai" probability. The "Tile" column and the "Disc" column (represents which tile is an unnecessary tile) are output only when the number of hand tiles is 3*N*+2 where *N* is natural number.

> **NOTE**: Winning probabilities and tempai probabilities when discarding tiles that increase shangten number are not calculated.

### Examples
- Number of hand tiles: 13, Method: Strictly

```shell
$ ./calc1-recu
Enter 13 tiles.
2478m111999p11s1z
Enter Range
18

The shanten number is 1

Prb     Rdy
0.338418        0.864314

Time (msec.)    0
```

- Number of hand tiles: 13, Method: Montecarlo

```shell
$ ./calc1-prob
Enter 13 tiles.
2478m111999p11s1z
Enter Range
18

The shanten number is 1

Prb     Rdy
0.325134        0.864314

Time (msec.)    0
```

- Number of hand tiles: 14, Method: Strictly

```shell
Enter 14 tiles.
12478m111999p11s1z
Enter Range
18

The shanten number is 1

Tile    Disc    Prb     Rdy
1m      1       0.342166        0.866829
2m      0       0       0
4m      1       0.342166        0.866829
7m      0       0       0
8m      0       0       0
1p      0       0       0
9p      0       0       0
1s      0       0       0
1z      1       0.342166        0.866829

Time (msec.)    0
```

- Number of hand tiles: 14, Method: Montecarlo

```shell
Enter 14 tiles.
12478m111999p11s1z
Enter Range
18

The shanten number is 1

Tile    Disc    Prb     Rdy
1m      1       0.336082        0.866829
2m      0       0       0
4m      1       0.336082        0.866829
7m      0       0       0
8m      0       0       0
1p      0       0       0
9p      0       0       0
1s      0       0       0
1z      1       0.332432        0.866829

Time (msec.)    0
```

### Three Player Mahjong mode
Enable `THREE_PLAYER`.

Example:
```
$ cmake .. -DCMAKE_BUILD_TYPE=Release -DTHREE_PLAYER=on
```

## Remarks
- It has been confirmed to work with Bash on Ubuntu on Windows (Ubuntu 18.04). The CMake version used is 3.10.2, the compiler version is GCC 7.4.0.
