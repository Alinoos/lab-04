# Report-04

Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в прошлый раз. Настройте сборочные процедуры на различных платформах:

# Task 1

Используйте GitHub Actions для сборки на операционной системе Linux с использованием компиляторов gcc и clang

Копируем репозиторий из предыдущей ЛР:

```
$ git clone https://github.com/alinoos/lab-03 lab-04
$ cd ~/lab-04
$ git remote remove origin
$ git remote add origin https://github.com/alinoos/lab-04.git
```

И создаем папку со следующим путем: `~/lab-04/.github/workflows`
```
$ mkdir .github
$ cd ~/lab-04/.github
$ mkdir workflows
$ cd ~/lab-04/.github/workflows
```

```
$ cat >> Linux.yml << EOF
> EOF
$ nano Linux.yml
```

Содержимое файла Linux.yml:

```
name: CMake

on:
 push:
  branches: [master]
 pull_request:
  branches: [master]

jobs: 
 build_Linux:

  runs-on: ubuntu-latest

  steps:
  - uses: actions/checkout@v3

  - name: Configure Solver
    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

  - name: Build Solver
    run: cmake --build ${{github.workspace}}/solver_application/build

  - name: Configure HelloWorld
    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

  - name: Build HelloWorld
    run: cmake --build ${{github.workspace}}/hello_world_application/buildс
```

```
$ git add Linux.yml
$ git commit -m "Linux.yml - 1"
$ git push origin master
```

Сценарий выполнился! (Скриншот в конце)

# Task 2

Используйте GitHub Actions для сборки на операционной системе Windows

```
$ cat >> Windows.yml << EOF
> EOF
$ nano Windows.yml
```

Содержимое файла Windows.yml:

```
name: CMake

on:
 push:
  branches: [master]
 pull_request:
  branches: [master]

jobs: 
 build_Windows:

  runs-on: windows-latest

  steps:
  - uses: actions/checkout@v3

  - name: Configure Solver
    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

  - name: Build Solver
    run: cmake --build ${{github.workspace}}/solver_application/build

  - name: Configure HelloWorld
    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

  - name: Build HelloWorld
    run: cmake --build ${{github.workspace}}/hello_world_application/build
```

```
$ git add Windows.yml
$ git commit -m "Windows.yml - 1"
$ git push origin master
```

Сценнарий выполнился!

![4](https://github.com/Alinoos/lab-04/assets/126507425/25fc0671-6069-409f-8b86-c34981bba5da)
