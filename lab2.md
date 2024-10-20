Для начала нам нужно считать ip-адрес, и найти индекс первого символа точки:

```bash
input=($1)
index=(`expr index "$input" .`)
```

далее запускаем основной цикл:

```bash
i=0
while [ $index -ne 0 ]
do
    index=(`expr index "$input" .`)
    if [[ $index -eq 0 ]] then
        number=${input}
    else
        number=${input:0:index-1}
    fi
    input=${input:index}
    if [[ ($number -lt 0) || ($number -gt 255) ]] then
        echo "Invalid ip address"
        exit $ERR
    fi
    ip[$i]=$number
    : $((i = $i + 1))
done
```

здесь переменная ``` $i ``` является индекс в массиве ``` $ip ```, куда мы складываем распарсенные числа из строки ip-адреса

цикл продолжается, пока мы не получим индекс точки равный 0, что значит что точек больше не осталось в строке ip-адреса

В этом месте мы находим индекс следующей точки, и если он равен 0, то строка - последний 4 байт ip-адреса (число), иначе мы берем срез текущего байта (от начала и до индекса точки), и тоже получаем число:
```bash
index=(`expr index "$input" .`)
if [[ $index -eq 0 ]] then
    number=${input}
else
    number=${input:0:index-1}
fi
```
далее 'двигаем' строку на следующее число, делая срез от индекса точки до конца строки:
```bash
input=${input:index}
```
В следующем условии мы проверяем, лежит ли полученное число в диапазоне от 0 до 255, и если не лежит, выходим с ошибкой ```$err```:
```bash
if [[ ($number -lt 0) || ($number -gt 255) ]] then
        echo "Invalid ip address"
        exit $ERR
fi
```
Далее, если проверки прошли, записываем число в массив ```$ip``` и двигаем индекс ```$i``` на 1:
```bash
ip[$i]=$number
: $((i = $i + 1))
```

Теперь проверяем что в массиве ```$ip``` обязательно лежит 4 числа:
```bash
if [[ ${#ip[@]} -ne 4 ]] then
    echo "Invalid ip address"
    exit $ERR
fi
```
После этого у нас в массиве ```$ip``` по индексам 0 1 2 3 лежат все байты ip-адреса, теперь необходимо перевести их в двоичный формат

Идем циклом по массиву ```$ip``` и передаем i-ый элемент в функцию  ```to_binary```, которая переводит число в двоичный формат и сразу выводит его:
```bash
for ((i=0;i<4;i++))
do
    to_binary ${ip[i]}
    if [[ $i -ne 3 ]] then
        echo -n '.'
    fi
done

echo ""
```

Теперь последний этап, разберемся с функцией ```to_binary```:
```bash
function to_binary {
    index=8
    while [ $index -ne -1 ]
    do
        result[$index]=0
    : $((index = $index - 1))
    done
    num=$1
    index=0
    while [ $num -ne 0 ]
    do
        : $((ost = $num % 2))
        : $((num = $num / 2))
        result[$index]=$ost
        : $((index = $index + 1))
    done
    res_string="${result[@}"
    res_string=${res_string//' '}
    res_string=$(rev <<< "$res_string")
    echo -n $res_string
}
```

Здесь 1 цикл заполняет массив ```result``` нулями, каждый элемент этого массива отображает один байт переводимого числа:
```bash
index=8
while [ $index -ne -1 ]
do
    result[$index]=0
: $((index = $index - 1))
done
```
Далее мы просто по алгоритму переводим число в двоичное, результирующие биты записываем в массив ```result``` (в обратном порядке!):
```bash
num=$1
index=0
while [ $num -ne 0 ]
do
    : $((ost = $num % 2))
    : $((num = $num / 2))
    result[$index]=$ost
    : $((index = $index + 1))
done
```
Теперь, чтобы сделать из массива корректную двоичную строку, нужно сначала перевести массив в строку, где все значения идут через пробел:
```bash
res_string="${result[@}"
```
Затем удалить из этой строки все пробелы:
```bash
res_string=${res_string//' '}
```
И наконец развернуть это строку, потому что в массиве биты шли в обратном порядке:
```bash
res_string=$(rev <<< "$res_string")
```
И в конце вывод результата:
```bash
echo -n $res_string
```

Пример работы скрипта:

![image](https://github.com/user-attachments/assets/e2db1bd1-061e-483a-ac7e-2031348b84d2)
