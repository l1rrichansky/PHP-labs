# Лабораторная работа №10. СОЗДАНИЕ WEB-СТРАНИЦ
### Задание 10.1. Создать веб-страницу, на которой будет выведена надпись «Я знаю PHP!».
```php
<? echo "<h2>Я знаю PHP!</h2>";?>
```
![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/d147a65e-0da7-4d5a-85cd-cbe71bd58cbd)
### Задание 10.2. Задан массив согласно варианту. Вывести значения (не более 20) в виде маркированного нумерованного(варианты 1,3,5,7,9) и ненумерованного (варианты 2,4,6,8,10) списка. <i>Вариант 6</i>: птицы из красной книги
### Решение:
```php
<?php
        echo "<h2>Список птиц, занесенных в Красную книгу РБ</h2>";
        $x = array('Выпь большая','Выпь малая','Орлан-белохвост','Малый подорлик','Чёрный коршун','Обыкновенная кваква', 'Полевой конёк','Белоглазый нырок','Луток','Серый гусь','Шилохвость','Зелёный дятел','Трёхпалый дятел','Коростель','Малый погоныш','Белая куропатка','Серощёкая поганка','Обыкновенный зимородок','Сизоворонка','Большой кроншнеп','Большой улит','Гаршнеп','Кулик-сорока','Малая чайка','Болотная сова','Домовый сыч','Кобчик');
        echo"<ul>";
        for($i=0;$i<count($x);$i++){
            echo "<li>".$x[$i]."</li>";
            }
            echo "</ul>";
    ?>
```
![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/915fe579-3893-488e-874f-26bbe25a70fc)
### Задание 10.3. Создать функцию, которая формирует и выводит на экран меню. Входные данные – последовательности названий пунктов и соответст-вующих им URL. Использовать функцию в скрипте, для вывода меню.
### Решение:
```php
<?php 
            function show_array($str){
                $array = explode(";",$str);
                for($i=0;$i<count($array);$i+=2){
                    echo "<li><a href='".$array[$i+1]."' target='_blank'>".$array[$i]."</li>";
                }
            }
            print_r($array[2]);

            show_array("Первое задание;1.php;Второе задание;2.php;Третье задание (Вы здесь);3.php;Моя страничка Вконтакте;http://vk.com/kirilllgolev");
        ?>

```
![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/2c2638df-9296-4fba-b22e-1489e93c6fad)
# Лабораторная работа №11. ПОЛУЧЕНИЕ И ОБРАБОТКА ДАННЫХ ИЗ ПОЛЬЗОВАТЕЛЬСКИХ ФОРМ
### Пример. Передача данных

```html
<form action="" method="POST">
Ваше имя <input type="text" name="name"><br>
Ваша фамилия <input type="text" name="surname"><br>
<input type="checkbox" name="version">расширенная версия<br>
<input type="submit" name="button" value="Да! ">
</form>
```
```php
<?php 
if (isset($_POST["button"])){// если нажали на кнопку с именем button
echo "Поздравляю, ".$_POST['name']." ".$_POST['surname']. ",<br>
скрипт, передающий данные из формы, заработал! ";
if (isset($_POST["version"])) echo "Выбрана расширенная версия.";
}
?>
```
### Задание 11.1. 

### Создать PHP-страницу для решения следующей задачи. Банк предлагает три вида вкладов: «30 дней 4 % годовых», «90 дней 4,5 % годовых», «150 дней 5 % годовых». Пользователям, имеющим счета в банке, предоставляется бонус в размере 0,3 % годовых. Разработать скрипт для расчета суммы начисленных процентов и итоговой суммы к выдаче в зависимости от введенной пользователем суммы.
Формула для расчета суммы начисленных процентов:

$$P=\frac{M\*n\*i}{36500}$$

Формула для расчета суммы к выдаче:

$$S=(\frac{n*i}{36500}+1)*M$$

Где	$S$ – сумма к выдаче, $P$ – сумма начисленных процентов, $i$ – ставка(% годовых), $n$ – количество дней вклада, $M$ – сумма вклада.

### Решение:

```html
<body>
    <form action="" method="POST">
        <table>
            <tr style="text-align: center;">               
                <td colspan="2" id='titt' >
                    <select name="sel" class="seleccc">
                        <option value="1">30 дней 4% годовых</option>
                        <option value="2">90 дней 4,5% годовых</option>
                        <option value="3">150 дней 5% годовых</option>
                    </select>
                </td>
            </tr>
            <tr>
                <td>
                    Сумма вклада 
                </td>
                <td class="right">
                    <input type="text" name="sum" id='sumvkl' autocomplete="off" maxlength="7"><br>
                </td>
            </tr>  
```
```php
<?php
            $n = 30;
            $i = 4;
            $text = '30 дней 4% годовых';           
            $m = 1000;
            $p = round(($i/36500)*$n*$m, 1);
            $s = round(((($i/36500)*$n)+1)*$m, 1);  
            if (isset($_POST["button"])){// если нажали на кнопку с именем button
                switch($_POST['sel']){
                    case 1:
                        $n = 30;
                        $i = 4;
                        $text = '30 дней 4% годовых';
                        break;
                    case 2:
                        $n = 90;  
                        $i = 4.5; 
                        $text = '90 дней 4,5% годовых';
                        break;                   
                    case 3:
                        $n = 150;
                        $i = 5; 
                        $text = '150 дней 5% годовых';
                        break;                    
                }
                $m = abs($_POST['sum']);
                if($m==0){
                    $m=0;
                }
                $p = round(($i/36500)*$n*$m, 1);
                $s = round(((($i/36500)*$n)+1)*$m, 1);
            }
                echo  "</tr>
                    <td colspan='2' style='text-align:center; color:#93c4a0;'>
                        ".$text." ".$m." руб. 
                    </td>
                </tr>";
                echo "<tr>
                    <td>
                        Сумма начисленных процентов
                    </td>
                    <td class='right'>
                    ".$p." руб.
                    </td>
                </tr>
                <tr>
                    <td>
                        Сумма к выдаче
                    </td>
                    <td class='right'>
                        ".$s." руб.
                    </td>
                </tr>"  ; 
            ?>
```
```html
</tr>
                <td colspan="2" style='text-align:center'>
                    <input type='submit' name='button' value='Вычислить'>
                </td>
            </tr>
        </table> 
    </form>    
</body>
```
![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/432bc696-6b4f-4671-8819-ea103c2ffa52)

# Лабораторная работа №12. РАЗРАБОТКА WEB-СТРАНИЦ С ИСПОЛЬЗОВАНИЕМ СЕССИЙ И COOKIES

### Задание 12.1.	Спросите у пользователя телефон с помощью формы. Затем сделайте так, чтобы в другой форме (поля: имя, фамилия, телефон) при ее открытии поле телефон было автоматически заполнено.
### Решение:
#### 1 форма
```php
<body>                
    <form name='f' action='' method="POST">
        <table>
            <tr>
                <td>Введите ваш номер телефона</td>
                <td><input type="number" name='tel' ></td>
            </tr>
            <tr>
                <?php 
                    if(isset($_POST['tel'])){
                        setcookie("tel",$_POST["tel"], time()+600);
                        echo "<td colspan=2 class='message'>Номер телефона сохранен</td>";
                    }
                ?>
            </tr>    
        </table>
    </form>
    <a href="1_1.php">Следующая форма</a>
    <a href="/13">Домашняя страница</a>
</body>
```
#### 2 форма
```php
<body>
    <form>
        <table>
            <tr>
                <td>Имя</td>
            
                <td><input type="text"></td></tr><tr>
                <td>Фамилия</td>
                <td><input type="text"></td></tr> <tr>
                <td>Номер телефона</td>
                <td><input type="number" <?php if($_COOKIE['tel']){echo "value='".$_COOKIE["tel"]."'";}?>></td></tr>
        </table>       
    </form>
    <a href="1.php">Предыдущая форма</a>
    <a href="/13">Домашняя страница</a>
</body>
```

### Результат:
![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/2e384237-0770-460a-b5c7-b6f7269187fc)
![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/bf9e5cb5-a0c4-488e-adaa-14f57830df08)

### Задание 12.2. Спросите дату рождения пользователя. При следующем заходе на сайт напишите сколько дней осталось до его дня рождения. Если сегодня день рождения пользователя - поздравьте его!
### Решение:
#### 1 форма
```php
<body>
    <form action="" method='POST'>
        <table>
            <tr>
                <td colspan='2'>
                    <input type='date' name='date'>
                    <input type="submit">
                </td>
            </tr>
        
    <?php 
        if(isset($_POST['date']))
        {
            setcookie("date", date('Y-m-d', strtotime($_POST['date'])));          
            setcookie("daydate",date('z', strtotime($_POST['date'])), time()+600);
            echo "<tr><td colspan='2'>Дата вашего рождения сохранена ".$_POST['date']."</td></tr>";
        }       
        
    ?>
    </table>
    </form>
    <a href="2_2.php">Следующая страница</a>
    <a href="/13">Домашняя страница</a>
</body>
```
#### 2 форма
```php
<body>
<?php        
    $adate = $_COOKIE['daydate'];
    $curday = getdate()['yday'];
    if($adate>$curday){
        $bruh = $adate-$curday;
    }
    else if($curday>$adate){
        $bruh = 365-($curday-$adate);
    }
    else{
        $bruh = 0;
    }
    if($bruh!=0){
        echo "<p>Счетчик дней до вашего дня рождения</p><div class='count'>".$bruh."</div>";
    }
    else{
        echo "<div class='count'>С Днем Рождения!</div>";
    }
    ?>
    <a href="2.php">Предыдущая форма</a>
    <a href="/13">Домашняя страница</a>
</body>
```
### Результат:

![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/b251c2cc-06ba-4af8-be99-ae582b754653)
![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/f9d3549b-c154-4057-bdb3-8954937bb906)

# Лабораторная работа №13. ИСПОЛЬЗОВАНИЕ СРЕДСТВА ЯЗЫКА PHP ДЛЯ РАБОТЫ С СУБД.
### Задание 13.1
![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/5d379d46-a5f4-4218-8a5c-a5730995fd50)
### Решение:
#### config.php
```php
<?php 
    $dsn = 'mysql:host=localhost; port=3306; dbname=shop';
    $pdo = new PDO($dsn, 'root', '');
?>
```
#### 1.php
```php
<body>
    <table>
        <tr><td colspan=2>
            <form name='f' action='' method="POST">
                <select name='s' onchange="this.form.submit()">
                    <?php              
                        $months = array('Январь','Февраль','Март','Апрель','Май','Июнь','Июль','Август','Сентябрь','Октябрь','Ноябрь','Декабрь');
                        for($i=0;$i<count($months);$i++)
                            {
                            echo "<option value=",($i+1);
                            if($_POST['s']==($i+1)){
                                echo ' selected';
                            }
                            echo ">",$months[$i],"</option>";}
                    ?>
                </select>
            </form>
        </td></tr>                    
    <?php
        if(isset($_POST['s'])){
        }
        else{
            $_POST['s']=1;
        }
        setcookie('month',$_POST['s'], time()+600);
        require 'config.php';
        $sql = "SELECT category, sum(price) FROM `orders` where month(date) = :mon GROUP BY `category`";
        $sql2 = "SELECT min(price), max(price), round(avg(price)), count(*)  FROM `orders` where month(date) = :mon";
        $query = $pdo->prepare($sql);
        $query->execute(['mon'=>$_POST['s']]);
        $query2 = $pdo->prepare($sql2);
        $query2->execute(['mon'=>$_POST['s']]);
        $roww = $query2->fetchALL(PDO::FETCH_ASSOC)[0];
        if($roww['count(*)']==0){
            echo "<tr><td colspan=2 style='text-align:center'>Заказов в этом месяце не было</td></tr>";
        }
        else{
            echo "<tr><td>Количество заказов </td><td style='text-align:right'>".$roww['count(*)']."</td></tr>";
            echo "<tr><td colspan=2>Выручка по категориям</td></tr><tr><td colspan=2><ul>";
            foreach(($query->fetchALL(PDO::FETCH_ASSOC)) as $row){
                echo '<li>'.$row['category'].' - '.$row['sum(price)'].' руб.</li>';
            }
            echo "</ul></td></tr>";
            echo "<tr><td>Средняя стоимость заказов </td><td>".$roww['round(avg(price))'].' руб.</td></tr>';
            echo "<tr><td>Минимальная стоимость заказа </td><td>".$roww['min(price)'].' руб.</td></tr>';
            echo "<tr><td>Максимальная стоимость заказа </td><td>".$roww['max(price)'].' руб.</td></tr>';  
        }                                        
    ?>
    </table>
</body>
```
### Результат:

![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/bb4d4266-ac26-4bbb-b995-6c6c99b17452)
![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/ffa9ac76-899c-4bbc-87ca-c217aa430f61)
![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/0a409a71-ac2c-406d-b9fc-a1aa0e708d40)

# Лабораторная работа №14. 
### Задание 14.1. Класс Студент, члены класса: ФИО, шифр группы, оценки по предметам(не меньше 5 предметов), номер курса. Методы: вычисление среднего балла, определение долгов(оценки ниже 4), определение решения об отчислении (количество долгов больше 3). Класс-наследник Дипломник имеет свойства: тема диплома, оценка по диплому. Методы: допуск к защите (количество долгов меньше 3), сдача диплома (при оценке больше 4).

### Решение:
```php
<body>
<?php
class student{
    public $fio;
    public $group;
    public $marks;
    public $course;
    function __construct($fio, $group, $marks, $course)
    {
        $this->fio = $fio;
        $this->group = $group;
        $this->marks = $marks;
        $this->course = $course;
    }
    function displayStudent(){
        echo "$this->fio<br>$this->group<br>";
        foreach($this->marks as $n => $m){
            echo "$n $m<br>";
        }
        echo "$this->course курс<br>";
    }
    function gpa(){
        $sum = 0;
        $count = 0;
        foreach($this->marks as $n => $m){
            $sum += $m;
            $count++;
        }
        $sum /= $count;
        echo "Средний балл: $sum<br>";
    }
    function debts(){
        $c = 0;
        echo "Долги<br>";
        foreach($this->marks as $n => $m){
            if($m<4){
                echo "$n $m<br>";
                $c++;
            }          
        }
        if($c==0)
        echo "Долгов нет<br>";
    }
    function dropout(){
        $c = 0;
        foreach($this->marks as $n => $m){
            if($m<4){
                $c++;
            }          
        }
        if($c>3){
            echo "Стоит вопрос об отчислении<br>";
        }
        else{
            echo "Пока что отчислять не собираются<br>";
        }
    }
}
class diploma extends student{
    public $topic;
    public $diplomaMark;
    function __construct($fio, $group, $marks, $course, $topic, $diplomaMark)
    {
        parent::__construct($fio, $group, $marks, $course);
        $this->topic = $topic;
        $this->diplomaMark = $diplomaMark;
    }
    function displayStudent(){
        parent::displayStudent();
        echo "Оценка по диплому: $this->diplomaMark<br>";
    }
    function admission(){
        $c = 0;
        foreach($this->marks as $n => $m){
            if($m<4){
                $c++;
            }          
        }
        if($c<3){
            echo "Допущен к защите<br>";
        }
        else{
            echo "Не допущен к защите<br>";
        }
    }
    function graduation(){
        if($this->diplomaMark<4){
            echo "Диплом не сдан :(<br>";
        }
        else{
            echo "Диплом сдан. Ура!<br>";
        }
    }
}
$bruh = new student('Голев Кирилл Олегович', 'ПО912', ['Математика'=>7,'КПиЯП'=>2,'ПОССиЯМ'=>9,'ПОММС'=>10,'Русский язык'=>7], 3);
$bruh->displayStudent();
$bruh->gpa();
$bruh->debts();
$bruh->dropout();
$artem = new diploma('Петрович Артем Андреевич', 'ПО912', ['Математика'=>5,'КПиЯП'=>10,'ПОССиЯМ'=>6,'ПОММС'=>5,'Русский язык'=>3], 3, 'ИКС "Почта"', 10);
$artem->displayStudent();
$artem->admission();
$artem->graduation();
?>
</body>
```

### Результат:
![image](https://github.com/l1rrichansky/PHP-labs/assets/85824228/6de713bb-2802-435c-9dcb-283d3f8f1a9b)
