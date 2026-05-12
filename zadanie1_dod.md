# Zadanie 1

## Analiza bezpieczeństwa obrazu przy użyciu Docker Scout

Bezpieczeństwo obrazu, pod kątem podatności, zweryfikowano narzędziem Docker Scout, uzyskując wynik 0C, 0H, 0M, 0L. Całkowity brak podatności wynika z użycia obrazu scratch, w którym nie ma systemu ani zbędnych plików. W kontenerze została tylko sama odizolowana aplikacja, co całkowicie eliminuje źródła potencjalnych zagrożeń.

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

## Konfiguracja Buildx do budowania obrazów wieloplatformowych

```
docker buildx create --name mybuilder --driver docker-container --use --bootstrap
```
<img width="945" height="161" alt="image" src="https://github.com/user-attachments/assets/21da9ddc-69f8-4737-9de0-5169bd5b172d" />

## Proces generowania obrazów Multi-arch

```
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t docker.io/niro514/test:lab_multi \
  --ssh default=/c/Users/Weronika/.ssh/gh_lab6_ed25 \
  --push \
  --cache-to type=registry,ref=docker.io/niro514/test:cache,mode=max \
  --cache-from type=registry,ref=docker.io/niro514/test:cache \
  -f Dockerfile_multi .
```
<img width="1090" height="258" alt="image" src="https://github.com/user-attachments/assets/fccf8870-c3c2-468c-80c3-dad7e61cbba8" />

Widoczny błąd wynika z braku wcześniej zapisanego cache'u w rejestrze, co jest sytuacją naturalną podczas pierwszego budowania obrazu i nie przeszkadza w poprawnym zakończeniu procesu.

<img width="1090" height="701" alt="image" src="https://github.com/user-attachments/assets/3483d3ed-d832-40d6-9445-9d213e41fc65" />

## Weryfikacja struktury manifestu oraz poprawności wykorzystania danych Cache

```
docker buildx imagetools inspect docker.io/niro514/test:lab_multi
```

Inspekcja manifestu potwierdziła poprawne utworzenie obrazu typu multi-arch obsługującego platformy linux/amd64 oraz linux/arm64
<img width="1090" height="458" alt="image" src="https://github.com/user-attachments/assets/9ebd1370-bf29-4d22-9537-54fa9deac9c2" />

Ponowne użycie komendy docker buildx w celu weryfikacji mechanizmu Cache
<img width="1090" height="671" alt="image" src="https://github.com/user-attachments/assets/b3bc15c6-59b3-4305-b686-a935b01c01ff" />



