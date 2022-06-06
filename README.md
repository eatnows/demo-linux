# Linux


## 리눅스 기본 명령어

### man (도움말 보기)
기본형식: `man <옵션> 키워드`

| Option              | Description                                                                                                                                                    |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -k                  | 매뉴얼 목록을 검색                                                                                                                                                     |
| -s [section-number] | (-s는 생략 가능하여 섹션 번호만 입력할 수 있음) <br/>입력한 섹션에서 메뉴얼 검색해서 출력 <br/> (1) User Commands <br/>(2) System Calls<br/>(3) Subroutines<br/>(4) Devices<br/>(5) File Formats |

| Key    | Description |
|--------|-------------|
| space  | next page   |
| enter  | next line   |
| b      | backward    |
| q      | quit        |

```
$ man ls
$ man -k delete
$ man -s userdel
```


### ls (파일 목록 보가)
특정 디렉토리 안의 파일 목록을 출력하는 커맨드이고 디렉토리 자체에 대한 설명이 필요할 땐 `-d` 옵션을 사용해야합니다.

기본형식: `ls <옵션> <파일|디렉토리>`

옵션이 굉장히 많지만 기본적인 4개의 옵션

| Option | Description                                                                                                               |
|--------|---------------------------------------------------------------------------------------------------------------------------|
| -a     | dot(.)으로 시작하는 숨겨진 파일까지 모두 출력                                                                                              |
| -l     | (long list) 파일/디렉토리의 자세한 정보(type, permission, link, size, owner) <br/> `-rwsr-xr-x 1 root root 68208  7월 15  2021 passwd` |
| -d     | 디렉토리 내용이 아닌 디렉토리 자체를 출력                                                                                                   |
| -R     | 하위 디렉토리까지 모두 출력                                                                                                           |

```
$ ls
$ ls -l
$ ls -a
$ ls -l /tmp
$ ls -ald /tmp
$ ls -R /usr/local
```


### mkdir (디렉토리 생성)
디렉토리를 생성

기본형식: `mkdir <옵션> <디렉토리_이름>`

| Option | Description                                            |
|--------|--------------------------------------------------------|
| -m     | 퍼미션 설정                                                 |
| -p     | 부모 디렉토리가 존재하지 않으면 부모 디렉토리(parent directories) 까지 같이 생성 |
```
$ mkdir /home/ubuntu/bin
$ mkdir ~/tmp-dir
$ mkdir -p ~/dir/subdir/subsubdir
$ mkdir -m 777 share
```


### rmdir (remove directory)
empty 디렉토리를 삭제

기본형식: `rmdir <옵션> <디렉토리_이름>`

| Option | Description             |
|--------|-------------------------|
| -p     | 비어있는 부모 디렉토리가 있으면 함께 삭제 |
```
$ rmdir /home/ubuntu/bin
$ rmdir ~/tmp-dir
$ rmdir -p ~/dir/subdir/subsubdir
$ rmdir share
```


### cd (change directory)
특정 디렉토리로 이동

기본형식: `cd <디렉토리_이름>`

| Argument | Description            |
|----------|------------------------|
| ~        | HOME 디렉토리로 이동          |
| -        | Previous directory로 이동 |

```
$ cd /tmp
$ cd /usr/bin
$ cd ~; pwd
$ cd
$ cd ..
$ cd $HOME
```


### cp (copy)
원본파일을 현재 또는 다른 디렉토리에 목적지파일이름으로 복사 <br>

기본형식: `cp <옵션> 원본파일이름 목적지파일이름`

| Option | Description                                  |
|--------|----------------------------------------------|
| -i     | (interactive) 복사할 때 덮어쓰기(overwrite) 할 것인지 질문 |
| -f     | 복사할 때 무조건 덮어쓰기                               |
| -r     | 디렉토리 복사                                      |

`.`을 사용하면 현재 디렉토리에 이름까지 그대로 복사가 됩니다
```
$ cp /etc/hosts .
```
여러개를 한번에 복사할 수도 있는데 `cp` 명령어 뒤에 공백을 구분으로 복사할 파일을 나열하면 된다. 단 마지막에는 복사되는 위치를 명시해주어야 합니다.
```
$ cp /etc/passwd /etc/hosts conf.d
```

디렉토리를 복사할 때는 반드시 `-r` 옵션을 사용해야 디렉토리가 디렉토리로 하위 디렉토리의 내용까지 담아서 복사할 수 있습니다.
```
$ cp -r conf.d conf.d.backup
```

linux는 기본적으로 파일을 복사, 이동할 때 덮어쓰기가 활성화가 됩니다. 
덮어쓰기 유무를 선택하고 싶을때는 `-i` 옵션을 사용하면 됩니다. overwrite 하겠냐는 질문에 `y` 혹은 `yes`를 하지않으면 덮어쓰기가 되지 않습니다.


### mv (move)
파일의 이름을 바꾸거나 다른 디렉토리로 이동

기본형식: `mv <옵션> 원본파일이름 새이름`

1. 디렉토리의 이름을 `새이름`에 명시해주게 되면 **이동**이됩니다. <br> 
2. 하지만 단순히 파일이름만 포함이 되어 있다면 **파일의 이름만 변경**하게 됩니다.

| Option | Description                                     |
|--------|-------------------------------------------------|
| -i     | (interactive) 이름을 바꿀 때 덮어쓰기(overwrite) 할 것인지 질문 |
| -f     | 이름을 바꿀 때 무조건 덮어쓰기                               |

```
$ mv hosts hosts.file
$ mv -i passwd hosts.file
$ mv passwd /tmp/passwd
$ mv conf.d setup.d
```

### rm (remove)

파일이나 디렉토리를 삭제

기본형식: `rm <옵션> 파일이름 or 디렉토리이름`

| Option | Description              |
|--------|--------------------------|
| -i     | 파일을 삭제할 때 삭제 여부를 한 번더 질문 |
| -f     | 파일을 삭제할 때 질문없이 무조건 삭제    |
| -r     | 하위내용을 포함한 디렉토리를 삭제       |

```
$ rm hosts.file
$ rm -i /tmp/passwd
$ rm setup.d
$ rm -rf setup.d
```
`rmdir`은 비어있는 디렉토리를 지우는 명령어 였지만 `rm`도 디렉토리를 삭제할 수 있습니다. <br>
하지만 `$ rm 디렉토리이름`으로 디렉토리를 삭제할 경우 디렉토리이기 때문에 삭제할 수 없다는 경고문이 뜬다. 이럴 경우 `-r` 옵션을 사용하면 됩니다.








