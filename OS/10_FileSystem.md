# File System

> 2020.10.27



## 1. File System

> 정의 : 디스크에서 파일 저장 및 검색을 담당하는 OS 모듈이다.
>
> 기능 : 파일과 관련된 API를 제공한다. 파일 무결성(데이터베이스에 저장된 데이터의 일관성을 의미한다. 데이터의 입력이나 변경 등을 제한하여 데이터의 안전성을 저해하는 요소를 막는다.)을 보장한다. 파일로의 빠른 접근을 가능하게 한다. 유저가 파일을 찾을 때 효율적인 방법을 제공한다.
>
> 목표 : 데이터의 손실을 없앤다. 데이터로의 빠른 접근을 가능하게 한다. 저장공간의 낭비를 최소화한다.



### 1.1 Physical layout of File System

​	![image-20201027161156540](.\img\FileSystem.jpg)

- Boot block : 부팅 코드를 저장한다.
- Super block : 메타데이터의 크기와 루트 디렉토리의 inode ID, Physical layout information of file system(bitmap의 시작 섹터, inode블락의 시작 섹터, data 블락의 시작 섹터)가 저장되어있다. 

- file : 파일 데이터와 메타데이터로 구성되어있다.
  - file data : 파일의 contents(내용)으로 data 블록에 저장되어있다.
  - file metadata : owner, size, modification time, access control information, locations of data block으로 inode 블록에 저장되어있다.
- directory : 디렉토리는 파일의 special type으로 간주되며, 파일과 동일하게 데이터와 메타데이터로 구성되어있다.
  - directory data : child file names와 inode IDs로 data 블록에 저장되어있다.
  - directory metadata : file metadata와 동일하다.

- inode block : inode는 file의 metadata를 담고 있으며, 파일 당 한 개 존재한다. 파일의 사이즈와 타입에 관계없이 inode의 사이즈는 고정되어있다. inode는 metadata를 담고 있기 때문에 inode를 알면 파일의 모든 정보를 알 수 있다. inode number는 0번 부터 시작하며 inode ID로 사용된다.

- data block : file data(name, inode ID)가 저장되어 있다.

  ![image-20201027164421969](.\img\inode.jpg)

- Bitmap block : inode bitmap과 data bitmap으로 구성되어 있다.
  - inode bitmap : inode block의 할당여부를 나타내며, file의 maximum number가 inode bitmap size에 의해 결정된다.
  - data bitmap : data block의 할당여부를 나타낸다.



### 1.2 File System API

- Create() : file을 생성하는 interface로 free inode를 찾아 metadata를 저장한다. (bitmap 사용)
  1. root inode와  root data block을 찾는다.
  2. root data block에 해당 파일이 존재하는지 확인한다.
  3. 존재하지 않는다면, bitmap block을 사용하여 free inode를 찾고 해당 inode에 저장할 파일의 메타 데이터를 저장한다.
  4. 사용한 inode를 이용해 data block으로 접근하여 file data를 저장한다.
- Open() : 현재 directory 혹은 root directory의 inode를 사용하여 target file의 inode를 찾는다.
  1. root inode와  root data block을 찾는다.
  2. data block에서 찾을 파일명과 inode ID를 찾는다.
  3. 찾은 inode를 메모리에 load한다.
  4. 찾은 inode의 파일 테이블을 생성한다.
- Read() : open()으로 찾은 inode를 사용하여 file content를 읽어온다.

- Write() : open()으로 찾은 inode를 사용하여 file content를 쓴다.



##  2. Secondary Storage



### 2.1 Logical Disk Structure

