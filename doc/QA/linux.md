# Linux

## 1. 文件系统指令
## 1.1 压缩与解压缩
### 1.1.1 zip 指令
-  压缩
   1.  **使用 `zip` 压缩文件**
        ```bash
        zip -r coco.zip coco
        ```

       - `r` 选项表示递归压缩目录。
       - `coco.zip` 是压缩后的文件名
       - `coco` 是要压缩的文件或目录


   2. **使用 `split` 命令分割压缩文件**
        ```bash
        split -b 5G coco.zip "coco.zip.part"
        ```

        - `-b 5G` 表示将数据分割为 5GB 大小的块。
        - `coco.zip` 是之前压缩的文件。
        - `"coco.zip.part"` 是分割文件的前缀，生成的分割文件将以 `coco.zip.partaa`、`coco.zip.partab`、`coco.zip.partac` 等命名。

- 解压缩
    1. **合并分割的zip文件**
        ```bash
        cat coco.zip* > coco.zip
        ```
    
    2. **解压缩合并后的文件**
        ```bash
        unzip coco.zip -d /path/to/your/directory
        ```
       - `-d /path/to/your/directory`：指定解压到的目标目录。
       - `split.zip`：合并后的 zip 文件。


### 1.1.2 tar 指令
-  压缩
    ```bash
    tar -zcf - coco | split -b 5G -d -a 2 - coco.tar.gz.
    ```

   1.  `tar -zcf - coco`

         - `tar` 命令用于打包和压缩文件或目录，`-z` 表示使用 gzip 压缩，`-c` 表示创建一个新的 tar 包，`-f` 后接 `-` 表示将输出直接发送到标准输出，而不是写入一个文件。
         - `coco` 是要被打包和压缩的文件或目录名。
         - 这部分的作用是将 `coco` 文件（或目录）压缩成 gzip 格式的流，并传递给下一个命令。

   2. `| split -b 5G -d -a 2 - coco.tar.gz`

       - `split` 命令将通过管道传递过来的流数据进行分割。
       - `-b 5G` 表示将数据分割为 5GB 大小的块。
       - `-d` 表示使用数字后缀（例如 .00、.01、.02 等）来命名分割后的文件。
       - `-a 2` 指定后缀的长度为 2，因此分割文件会被命名为 `coco.tar.gz00`、`coco.tar.gz01`、`coco.tar.gz02` 等。

       -  `-` 表示从标准输入读取数据，这里是从 `tar` 命令传递过来的流数据。
       - `coco.tar.gz` 是分割文件的前缀。

- 解压缩
    1. **合并分割的文件**
        ```bash
        cat coco.tar.gz* > coco.tar.gz
        ```
       - 这条命令将所有以 `coco.tar.gz` 开头的分割文件合并成一个名为 `coco.tar.gz` 的完整文件。`cat` 会按文件的字母顺序读取文件并将它们合并。
    
    2. **解压缩合并后的文件**
        ```bash
        tar -zxvf coco.tar.gz -C /path/to/your/directory
        ```
        - `-z` 表示使用 gzip 解压。
        - `-x` 表示解压缩文件。
        - `-v` 表示显示解压过程中的详细信息（可选）。
        - `-f` 后跟文件名，指定要解压的文件。
        - `-C` /path/to/your/directory：表示将文件解压到 /path/to/your/directory 目录中。

## 1.2 文件夹大小与数量
- `du -sh`：查看当前目录的总大小。
    ```bash
    du -sh directory_name
    ```
   - `-s`：表示只显示目录总大小。
   - `-h`：以易读的格式（KB, MB, GB）显示。

- `du -ah`：列出目录中每个文件的大小。
    ```bash
    du -ah directory_name
    ```

- 获取目录中的文件和子目录数量
    ```bash
    ls -1 /path/to/directory | wc -l
    ```
    - `ls -1`：列出目录中的所有内容，每行一个文件或目录。
    - `wc -l`：统计行数，即文件和子目录的数量。