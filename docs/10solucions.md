# Solucions

## Tema 2: Introducció a PHP

#### Exercici 1: Manipulació de Variables i Operadors

Assigna múltiples variables i utilitza operadors aritmètics i lògics. Mostra el resultat de cada operació.


```php
<html>
<?php 
    $a = 10;
    $b = 5;
    $c = 3;
?>    
<body>
    
    <table style='border: 1px solid'>
        <thead>
            <tr>
                <th>Operació</th>
                <th>a i b</th>
                <th>b i c</th>
                <th>a i c</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>+</td>
                <td><?= $a+$b ?></td>
                <td><?= $b+$c ?></td>
                <td><?= $a+$c ?></td>
            </tr> 
            <tr><td>-</td><td><?= $a-$b ?></td><td><?= $b-$c ?></td><td><?= $a-$c ?></td></tr> 
            <tr><td>*</td><td><?= $a*$b ?></td><td><?= $b*$c ?></td><td><?= $a*$c ?></td></tr> 
            <tr><td>/</td><td><?= $a/$b ?></td><td><?= $b/$c ?></td><td><?= $a/$c ?></td></tr> 
        </tbody>        
    </table> 

</body>
</html>
```

#### Exercici 2: Control de Flux amb Bucles

Utilitza un bucle `for` per imprimir els números parells del 0 al 20.
Fes-ho també amb un bucle `while`.

```php
 <html>
    <body>
        <ul>
            <?php
            for($i=2;$i<20;$i=$i+2){
            ?>    
                <li><?= $i ?></li>
            <?php    
            }
            ?>
            <?php
           
            do {
                echo "<li>$i</li>";
                $i = $i -2;
            } while ($i>0)
            ?>
        </ul>
    </body>
</html>
```


#### Exercici 3: Treballar amb Arrays i Funcions

Escriu una funció que prenga un array de números, calculi la mitjana i retorni el resultat. Utilitza aquesta funció per imprimir la mitjana d'un array de cinc números.

```php
<?php 
include_once "helpers/funciones.php";

$numeros = array(45,3,46,7,8,9,12,90);

echo media($numeros);
 
```

```php
<?php
function media(Array $numeros){
    return array_sum($numeros) / count($numeros);
}
```
 

#### Exercici 4: Manipulació de Strings

Escriu un script que prenga una cadena de text i compti el nombre de vocals. Imprimeix el resultat.

```php
<?php
include_once "helpers/funciones.php";

$cadena = "Men to the left beucase women are always right.AEIOU";

echo contar_vocales(strtolower($cadena));
```

```php
<?php
function contar_vocales($sentence){
    $vocales = ['a','e','i','o','u'];
    $total = 0;
    foreach ($vocales as $vocal){
        $total += substr_count($sentence,$vocal);
    }
    return $total;
}
```

#### Exercici 5: Arrays Multidimensionals

Crea un array multidimensional que represente una taula de multiplicar del 1 al 5 i imprimeix els resultats en forma de taula.

```php
<?php


$tabla = [];
$quantes = 13;
$fins = 60;


for ($i= 1; $i<= $quantes;$i++){
    for ($j=1 ; $j<= $fins; $j++){
        $tabla[$i][$j] = $i * $j;
    }
}

?>

<body> 
    <table style='border: 1px solid'>
        <thead>
            <tr>
                <th>Multiplicar</th>
                <?php
                for ($j = 1; $j<= $fins ; $j++){
                    ?>
                    <th><?= $j ?>
                <?php } ?>
            </tr>
        </thead>
        <tbody>     
            <?php for ($i = 1; $i<= $quantes ; $i++){ ?>
                <tr>
                <th><?= $i ?></th>
                <?php for ($j=1;$j<= $fins; $j++){ ?>
                    <td><?= $tabla[$i][$j] ?></td>    
                <?php } ?>
                </tr>
            <?php } ?>
        </tbody>        
    </table> 
</body>
</html>

```


#### Exercici 6: Utilitzant `match` per a categoritzar

Crea un fitxer que utilitze la instrucció `match` per categoritzar una variable `$nota` segons el següent criteri:
- Si la nota és 10, imprimir "Excel·lent".
- Si la nota és 8 o 9, imprimir "Molt bé".
- Si la nota és 5, 6 o 7, imprimir "Bé".
- Per qualsevol altra nota, imprimir "Insuficient".
    
```php
  <html>
    <body>
        <?php
     $nota = 7;

    $qualificacio= match (true) {
        $nota === 10 => 'Excel.lent',
        $nota >= 8 && $nota < 10 => 'Molt bé',
        $nota >= 5 && $nota < 8 => 'Bé',
        default => 'Insuficient',
    };

    echo $qualificacio;
    ?>
    </body>
</html>
```

#### Exercici 7: Validació de Formularis

Crea un formulari en HTML que permetis als usuaris introduir el seu nom, el correu electrònic i un password (dues vegades). Després de l'enviament del formulari, valida que tots els camps han estat completats i que el correu electrònic és vàlid, que el password tinga complexitat i que coincidixen. Mostra un missatge d'error si alguna validació falla, i si tot és correcte, mostra un missatge confirmant que l'usuari s'ha registrat correctament.

```php
<?php

// Funció per processar l'entrada
function test_input($data) {
    $data = trim($data);
    $data = stripslashes($data);
    $data = htmlspecialchars($data);
    return $data;
}

// Inicialitzar variables d'error i missatge de confirmació
$error = array();
$name = $email = $password = $confirmPassword = "";
$successMessage = "";

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Validar el nom
    if (empty($_POST["name"])) {
        $error['name'] = "El nom és obligatori";
    } else {
        $name = test_input($_POST["name"]);
    }

    // Validar el correu electrònic
    if (empty($_POST["email"])) {
        $error['email'] = "El correu electrònic és obligatori";
    } else {
        $email = test_input($_POST["email"]);
        if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
            $error['email'] = "El format del correu electrònic no és vàlid";
        }
    }

    // Validar la contrasenya
    if (empty($_POST["password"])) {
        $error['password'] = "La contrasenya és obligatòria";
    } else {
        $password = test_input($_POST["password"]);
        // Comprovar la complexitat de la contrasenya (mínim 8 caràcters, majúscula, minúscula i un número)
        if (!preg_match("/^(?=.*[A-Z])(?=.*[a-z])(?=.*\d).{8,}$/", $password)) {
            $error['password'] = "La contrasenya ha de tenir almenys 8 caràcters, una majúscula, una minúscula i un número";
        }
    }

    // Validar la confirmació de la contrasenya
    if (empty($_POST["confirm_password"])) {
        $error['confirm_password'] = "Has de confirmar la contrasenya";
    } else {
        $confirmPassword = test_input($_POST["confirm_password"]);
        if ($password !== $confirmPassword) {
            $error['confirm_password'] = "Les contrasenyes no coincideixen";
        }
    }

    // Si no hi ha errors, mostrar missatge d'èxit
    if (!count($error)) {
        $successMessage = "L'usuari s'ha registrat correctament!";
    }
}




?>

<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulari de registre</title>
</head>
<body>

<h2>Formulari de registre</h2>

<!-- Mostrar missatge d'èxit si l'usuari s'ha registrat -->
<?php if ($successMessage): ?>
    <p style="color: green;"><?= $successMessage; ?></p>
<?php else: ?>

<form method="post" action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>">
    Nom: <input type="text" name="name" value="<?= $name; ?>">
    <span style="color: red;"><?= $error['name']??''; ?></span>
    <br><br>

    Correu electrònic: <input type="text" name="email" value="<?php echo $email; ?>">
    <span style="color: red;"><?php echo $error['email']??''; ?></span>
    <br><br>

    Contrasenya: <input type="password" name="password">
    <span style="color: red;"><?php echo $error['password']??''; ?></span>
    <br><br>

    Confirmar contrasenya: <input type="password" name="confirm_password">
    <span style="color: red;"><?php echo $error['confirm_password']??''; ?></span>
    <br><br>

    <input type="submit" value="Registrar">
</form>
<?php endif; ?>

</body>
</html>
```

#### Exercici 8: Processament de Formularis amb Select i Radio Buttons

A partir del formulari [newBook.php](recursos/newBook.php), fes que el mòdul i el estat els agafe de valors introduïts en arrays. Mostra el resultat en una taula.

```php
<?php
// Arrays de valors per a "Mòdul" i "Estat"
$modules = ["mat" => "Matemàtiques","his" => "Història","cie" => "Ciències", "lit"=>"Literatura"];
$statuses = ["Disponible", "No disponible", "Pròximament"];

// Inicialitzar variables per emmagatzemar els valors introduïts
$module = $publisher = $price = $pages = $status = $comments = "";

// Comprovar si el formulari ha estat enviat
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $module = $_POST['module'];
    $publisher = $_POST['publisher'];
    $price = $_POST['price'];
    $pages = $_POST['pages'];
    $status = $_POST['status'];
    $comments = $_POST['comments'];
}
?>

<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <title>Alta Llibre</title>
    <style>
        .error {
            color: red;
        }
        table, th, td {
            border: 1px solid black;
            border-collapse: collapse;
            padding: 10px;
        }
    </style>
</head>
<body>

<form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>" method="post" enctype="multipart/form-data">
    <div>
        <label for="module">Mòdul:</label>
        <select id="module" name="module">
            <?php foreach ($modules as $key => $mod): ?>
                <option value="<?php echo $key; ?>"><?php echo $mod; ?></option>
            <?php endforeach; ?>
        </select>
    </div>
    
    <div>
        <label for="publisher">Editorial:</label>
        <input type="text" id="publisher" name="publisher" value="<?php echo $publisher; ?>">
    </div>

    <div>
        <label for="price">Preu:</label>
        <input type="text" id="price" name="price" value="<?php echo $price; ?>">
    </div>

    <div>
        <label for="pages">Pàgines:</label>
        <input type="text" id="pages" name="pages" value="<?php echo $pages; ?>">
    </div>

    <div>
        <label for="status">Estat:</label>
        <?php foreach ($statuses as $stat): ?>
            <input type="radio" name="status" value="<?php echo $stat; ?>" <?php if ($status == $stat) echo "checked"; ?>>
            <?php echo $stat; ?>
        <?php endforeach; ?>
    </div>

    <div>
        <label for="photo">Foto:</label>
        <input type="file" id="photo" name="photo">
    </div>

    <div>
        <label for="comments">Comentaris:</label>
        <textarea id="comments" name="comments"><?php echo $comments; ?></textarea>
    </div>

    <div>
        <button type="submit">Donar d'alta</button>
    </div>
</form>

<?php if ($_SERVER["REQUEST_METHOD"] == "POST"): ?>
    <h2>Dades introduïdes:</h2>
    <table>
        <tr>
            <th>Mòdul</th>
            <th>Editorial</th>
            <th>Preu</th>
            <th>Pàgines</th>
            <th>Estat</th>
            <th>Comentaris</th>
        </tr>
        <tr>
            <td><?php echo $modules[$module]; ?></td>
            <td><?php echo $publisher; ?></td>
            <td><?php echo $price; ?></td>
            <td><?php echo $pages; ?></td>
            <td><?php echo $status; ?></td>
            <td><?php echo $comments; ?></td>
        </tr>
    </table>
<?php endif; ?>

</body>
</html>
```

#### Exercici 9: Pujar imatges des de formulari

A partir del formulari anterior fes que es puga pujar una imatge. Mostra la imatge en la taula.

```php
<?php
// Arrays de valors per a "Mòdul" i "Estat"
$modules = ["Matemàtiques", "Història", "Ciències", "Literatura"];
$statuses = ["Disponible", "No disponible", "Pròximament"];

// Inicialitzar variables per emmagatzemar els valors introduïts
$module = $publisher = $price = $pages = $status = $comments = $imagePath = "";
$imageError = "";

// Comprovar si el formulari ha estat enviat
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $module = $_POST['module'];
    $publisher = $_POST['publisher'];
    $price = $_POST['price'];
    $pages = $_POST['pages'];
    $status = $_POST['status'];
    $comments = $_POST['comments'];

    // Gestionar la pujada de la imatge
    if (isset($_FILES['photo']) && $_FILES['photo']['error'] == 0) {
        // Definir el directori on es pujarà la imatge
        $targetDir = "uploads/";
        // Agafar el nom del fitxer
        $fileName = basename($_FILES["photo"]["name"]);
        $fileType = pathinfo($fileName, PATHINFO_EXTENSION);
        $permitted_chars = '0123456789abcdefghijklmnopqrstuvwxyz';

        $newFileName = substr(str_shuffle($permitted_chars), 0, 10).".$fileType";
        // Definir la ruta completa per guardar la imatge
        $targetFilePath = $targetDir . $newFileName;
        // Comprovar el tipus de fitxer
        
        // Permetre només imatges (formats png, jpg, jpeg, gif)
        $allowedTypes = ['jpg', 'jpeg', 'png', 'gif'];
        if (in_array(strtolower($fileType), $allowedTypes)) {
            // Intentar moure la imatge pujada al directori definit
            if (move_uploaded_file($_FILES["photo"]["tmp_name"], $targetFilePath)) {
                $imagePath = $targetFilePath;
            } else {
                $imageError = "No s'ha pogut pujar la imatge.";
            }
        } else {
            $imageError = "Només es permeten arxius de tipus JPG, JPEG, PNG, GIF.";
        }
    } else {
        $imageError = "Si us plau, selecciona una imatge per pujar.";
    }
}
?>

<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <title>Alta Llibre</title>
    <style>
        .error {
            color: red;
        }
        table, th, td {
            border: 1px solid black;
            border-collapse: collapse;
            padding: 10px;
        }
    </style>
</head>
<body>

<form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>" method="post" enctype="multipart/form-data">
    <div>
        <label for="module">Mòdul:</label>
        <select id="module" name="module">
            <?php foreach ($modules as $mod): ?>
                <option value="<?php echo $mod; ?>"><?php echo $mod; ?></option>
            <?php endforeach; ?>
        </select>
    </div>
    
    <div>
        <label for="publisher">Editorial:</label>
        <input type="text" id="publisher" name="publisher" value="<?php echo $publisher; ?>">
    </div>

    <div>
        <label for="price">Preu:</label>
        <input type="text" id="price" name="price" value="<?php echo $price; ?>">
    </div>

    <div>
        <label for="pages">Pàgines:</label>
        <input type="text" id="pages" name="pages" value="<?php echo $pages; ?>">
    </div>

    <div>
        <label for="status">Estat:</label>
        <?php foreach ($statuses as $stat): ?>
            <input type="radio" name="status" value="<?php echo $stat; ?>" <?php if ($status == $stat) echo "checked"; ?>>
            <?php echo $stat; ?>
        <?php endforeach; ?>
    </div>

    <div>
        <label for="photo">Foto:</label>
        <input type="file" id="photo" name="photo">
        <span class="error"><?php echo $imageError; ?></span>
    </div>

    <div>
        <label for="comments">Comentaris:</label>
        <textarea id="comments" name="comments"><?php echo $comments; ?></textarea>
    </div>

    <div>
        <button type="submit">Donar d'alta</button>
    </div>
</form>

<?php if ($_SERVER["REQUEST_METHOD"] == "POST" && empty($imageError)): ?>
    <h2>Dades introduïdes:</h2>
    <table>
        <tr>
            <th>Mòdul</th>
            <th>Editorial</th>
            <th>Preu</th>
            <th>Pàgines</th>
            <th>Estat</th>
            <th>Comentaris</th>
            <th>Imatge</th>
        </tr>
        <tr>
            <td><?php echo $module; ?></td>
            <td><?php echo $publisher; ?></td>
            <td><?php echo $price; ?></td>
            <td><?php echo $pages; ?></td>
            <td><?php echo $status; ?></td>
            <td><?php echo $comments; ?></td>
            <td>
                <?php if (!empty($imagePath)): ?>
                    <img src="<?php echo $imagePath; ?>" alt="Imatge del llibre" style="width: 100px;">
                <?php else: ?>
                    Sense imatge
                <?php endif; ?>
            </td>
        </tr>
    </table>
<?php endif; ?>

</body>
</html>
```

## Tema 3: Programació Web

