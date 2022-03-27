---
title: "[Linux 명령어] module"
date: 2022-03-27 23:16:00 +0900
categories: ["Linux"]
tags: ["Linux", "module"]
---

`module [_switches_] [_sub-command_ [_sub-command-args_]]`

Modules라는 패키지를 관리할 때 쓰는 명령어입니다.
Modules package는 사용자가 현재 개발 환경을 손쉽게 바꿀 수 있도록 도와주는 툴입니다.

예를 들어서 현재 컴퓨터에 gcc 9.4.0과 gcc 10.0이 깔려 있다고 합시다. $PATH에 gcc 9.4.0 의 경로가 들어 있다면, gcc 10.0을 사용하기 위해서는 $PATH를 변경해야 합니다. 다시 9.4.0을 쓰고 싶다면 한 번 더 $PATH를 변경해야겠죠.
이런 상황에서 일일이 환경변수를 건드리기 귀찮으니, `module load gcc/9.4.0` 혹은 `module load gcc/10.0` 같은 방식으로 손쉽게 **환경변수**를 바꿔주는 툴이 Modules package입니다.

mkl같은 외부 라이브러리는 설치 이후 module 명령어를 통해 환경변수를 설정하더라고요.

# module 사용법
`module avail`

사용할 수 있는 모든 모듈을 보여줍니다.

구체적으로 말하면, $MODULEPATH에 존재하는 모든 modulefiles를 보여줍니다.

예시 :
```terminal
$ module avail
-------------------------- /opt/intel/oneapi/modulefiles --------------------------
advisor/2021.3.0     compiler-rt/latest     dal/2021.3.0       dnnl-cpu-gomp/latest
dpct/2021.3.0        inspector/latest       mkl32/latest       tbb32/2021.3.0
... 생략
```
<hr>

`module use [-a|--append] directory...`

해당 directory에 있는 모듈을 인식합니다.

구체적으로 말하면, $MODULEPATH 앞에 해당 directory 경로를 추가합니다. `--append`의 경우는 뒤에 추가합니다.

예시 :
```terminal
$ module use /opt/intel/oneapi/modulefiles
```

<hr>

`module list`

현재 로드한 모듈을 보여줍니다.

예시 :
```terminal
$ module list
Currently Loaded Modulefiles:
 1) tbb/latest           3) mkl/latest   5) debugger/latest   ...생략
 2) compiler-rt/latest   4) mpi/latest   6) dpl/latest
```

<hr>

`module load modulefile...`

모듈을 로드합니다.

<hr>

`module unload modulefile...`

로드한 modulefile을 shell 환경에서 지웁니다.

<hr>

`module display modulefile...`

모듈 파일에 대한 정보를 보여줍니다.

예시 파일을 보면 조건에 따라 환경변수만을 바꾼다는 것을 짐작할 수 있네요.
```terminal
$ module display /opt/intel/oneapi/modulefiles/mkl/2021.3.0
-------------------------------------------------------------------
/opt/intel/oneapi/modulefiles/mkl/2021.3.0:

conflict        mkl32
conflict        mkl
module-whatis   {Intel(R) oneAPI Math Kernel Library (oneMKL) IA-64 architecture}
setenv          MKLROOT /opt/intel/oneapi/mkl/2021.3.0
prepend-path    LD_LIBRARY_PATH /opt/intel/oneapi/mkl/2021.3.0/lib/intel64
prepend-path    LIBRARY_PATH /opt/intel/oneapi/mkl/2021.3.0/lib/intel64
prepend-path    CPATH /opt/intel/oneapi/mkl/2021.3.0/include
prepend-path    PKG_CONFIG_PATH /opt/intel/oneapi/mkl/2021.3.0/tools/pkgconfig
prepend-path    NLSPATH /opt/intel/oneapi/mkl/2021.3.0/lib/intel64/locale/%l_%t/%N
```
<hr>

modulefile 작성법은 언젠간 다음 기회에...

참고 사이트<br>
[https://modules.readthedocs.io/en/latest/](https://modules.readthedocs.io/en/latest/)
[https://modules.readthedocs.io/en/latest/module.html](https://modules.readthedocs.io/en/latest/module.html)