---
layout: post
title: Shicontstand Laravel Package
date: 2022-11-07
categories: ["Developer", "Laravel", "Packeges"]
---

Tengo mucho tiempo desarrollando para el área de operaciones de almacenes en el sector portuario, específicamente con todo lo relacionado al inventario de contenedores marítimos, esto me tiene motivado en este momento para crear o automatizar ciertas funciones., que me sirvan a mis mismo para acelerar ciertos desarrollo o que ayuden a otros en sus propios desarrollos.


_Perdí la cuenta de las veces que he tenido que aplicar la_ `ISO 6346`., _este es el motivo por lo que cree_ **Shicontstand**

>ISO 6346 is an international standard covering the coding, identification and marking of intermodal (shipping) containers used within containerized >intermodal freight transport by the International Organization for Standardization (ISO)

# Shicontstand

<a href="https://packagist.org/packages/laymont/shicontstand" rel="nofollow noindex noopener external ugc"><img src="https://camo.githubusercontent.com/56b8853f759e8560a5776a8c3dec9c76a9a9af70a11db610f77f4ae5e44f215c/68747470733a2f2f696d672e736869656c64732e696f2f7061636b61676973742f762f6c61796d6f6e742f736869636f6e747374616e642e7376673f7374796c653d666c61742d737175617265" alt="Latest Version on Packagist"></a>
[![Total Downloads][ico-downloads]][link-downloads]
[![Build Status][ico-travis]][link-travis]
[![StyleCI][ico-styleci]][link-styleci]



The purpose of this package is to implement the ISO 6346 standard, which covers the coding, 
identification and marking of containers, used in intermodal freight transport.
The standard establishes a visual identification system for every container that includes a 
unique serial number (with check digit), the owner, a country code, a size, type 
and equipment category as well as any operational marks.

## Installation

Via Composer

``` bash
composer require laymont/shicontstand
```

Publish the config file with:

```bash
php artisan vendor:publish --tag="shicontstand-config"
```

This is the contents of the published config file:

> 1. ***You can alter tables name before run migrations., in tables section of next array*** 
> 2. ***Define the name of the property in your model that stores the number of the container, also defines the property that stores the iso code of the container*** 

```php
<?php
return [
    /**
     * The equipment category identifier consists of one of the following capital letters of the Latin alphabet
     */
    'equipment_category_identifier' => [
        ['u' => 'for all freight containers'],
        ['J' => 'for detachable freight container-related equipment'],
        ['Z' => 'for trailers and chassis'],
    ],

    /**
     * An equivalent numerical value is assigned to each letter of the alphabet,
     * beginning with 10 for the letter A (11 and multiples thereof are omitted)
     */
    'calculation_step_one' => [
        ['character' => 'A', 'value' => 10],
        ['character' => 'B', 'value' => 12],
        ['character' => 'C', 'value' => 13],
        ['character' => 'D', 'value' => 14],
        ['character' => 'E', 'value' => 15],
        ['character' => 'F', 'value' => 16],
        ['character' => 'G', 'value' => 17],
        ['character' => 'H', 'value' => 18],
        ['character' => 'I', 'value' => 19],
        ['character' => 'J', 'value' => 20],
        ['character' => 'K', 'value' => 21],
        ['character' => 'L', 'value' => 23],
        ['character' => 'M', 'value' => 24],
        ['character' => 'N', 'value' => 25],
        ['character' => 'O', 'value' => 26],
        ['character' => 'P', 'value' => 27],
        ['character' => 'Q', 'value' => 28],
        ['character' => 'R', 'value' => 29],
        ['character' => 'S', 'value' => 30],
        ['character' => 'T', 'value' => 31],
        ['character' => 'U', 'value' => 32],
        ['character' => 'V', 'value' => 34],
        ['character' => 'W', 'value' => 35],
        ['character' => 'X', 'value' => 36],
        ['character' => 'Y', 'value' => 37],
        ['character' => 'Z', 'value' => 38],
    ],

    /**
     * Each of the numbers calculated in step 1 is multiplied by 2position, where position is the exponent to base 2.
     * Position starts at 0, from left to right.
     * The following table shows the multiplication factors
     */
    'calculation_step_two' => [1, 2, 4, 8, 16, 32, 64, 128, 256, 512],

    /**
     * table names
     */
    'tables' => [
        'type_groups' => 'scs_type_groups',
        'size_types' => 'scs_size_types',
        'length_codes' => 'scs_length_codes',
        'size_codes' => 'scs_size_codes',
        'type_codes' => 'scs_type_codes',
    ],

    /**
     * Container Model name
     */
    'model' => [
        'name' => 'containers',
        'property' => 'number',
    ],

    /**
     * Route Configuration
     */
    'prefix' => 'scs',
    'middleware' => ['web'],
];
?>
```

publish and run the migrations with:
``` bash
php artisan vendor:publis --tag="shicontstand-migrations"
```

Publish Seeders after migrations done
``` bash
php artisan vendor:publis --tag="shicontstand-seeders"
```

Run seeders
``` bash
php artisan db:seed --class=ShicontstandSeeder
```

It is recommended to update the routes cache
```
php artisan route:cache
``` 
### for [more](https://github.com/laymont/Shicontstand) information
