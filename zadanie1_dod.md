# Zadanie 1

## Analiza bezpieczeństwa obrazu przy użyciu Docker Scout
```
docker scout quickview zadanie1:latest
```

<img width="1090" height="417" alt="image" src="https://github.com/user-attachments/assets/2bd9130a-02d1-4318-83e0-d115eaa27556" />

```
docker scout cves zadanie1:latest
```

<img width="1090" height="437" alt="image" src="https://github.com/user-attachments/assets/573d7b26-c146-4b0e-b189-6f93d3af9f9a" />

## Konfiguracja agenta SSH
```
eval $(ssh-agent -s)
```
<img width="498" height="88" alt="image" src="https://github.com/user-attachments/assets/7b257f75-2498-43d0-a860-b1619e5548b4" />
```
ssh-add /c/Users/Weronika/.ssh/gh_lab6_ed25
```
<img width="1090" height="105" alt="image" src="https://github.com/user-attachments/assets/37cdec8c-6ecd-481b-829b-2a0345c51a35" />

## Stworzenie repozytorium na GitHubie
```
cd "/r/6 sem/przylucki/z1nieob"
git init
```
<img width="988" height="188" alt="image" src="https://github.com/user-attachments/assets/349abcd8-1266-4cab-a93a-5db56025faa3" />
```
git add main.c Dockerfile_multi
```
<img width="959" height="173" alt="image" src="https://github.com/user-attachments/assets/8531a89b-9ba2-4187-b009-04599f4782aa" />
```
gh repo create lab_pogoda --public --source=. --remote=origin --push
```
<img width="1033" height="416" alt="image" src="https://github.com/user-attachments/assets/9ef989da-5bd3-44cd-a9d2-7e5b8b8e0e70" />

##



