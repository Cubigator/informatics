Задача 1
```bash
#!bin/bash
find . -type f -name "*.txt" | while read file; do
    if ! grep "Author:" "$file";
    then
        echo "Not find author at $file";
        exit 124234;
    fi
done
```

в false.txt нет подстроки "Author:":

![Снимок экрана 2024-12-15 205611](https://github.com/user-attachments/assets/a424fb6c-ecac-424d-8cf7-dd6897abb386)

Задача 2

![image](https://github.com/user-attachments/assets/d63aac3b-c604-4b38-acf1-220fcc10c20e)

![image](https://github.com/user-attachments/assets/773d4978-2dc7-4172-9293-320b6b64b5f5)

![image](https://github.com/user-attachments/assets/d6ddedb1-2534-4f46-9fcf-695533b3c2ad)

![image](https://github.com/user-attachments/assets/bdc186b6-56e3-49ec-9e61-762d6303081b)

![image](https://github.com/user-attachments/assets/3a3698a9-9296-4297-831a-a20fc5e481b7)

![image](https://github.com/user-attachments/assets/330b5e01-b13e-4670-96b4-0bb2694688fb)

![image](https://github.com/user-attachments/assets/51eeb99c-19f6-48ab-ba64-89de192463dd)

![image](https://github.com/user-attachments/assets/280e88f9-e4d6-4f74-b79b-3e2c87bfe00a)

![image](https://github.com/user-attachments/assets/f6599aa0-c984-498a-8b31-ffa44a0e6c7a)

