# Class, Object, Method, Package, dan Constructor

```
Procedural code (code using data structures) makes it easy
to add new functions without changing the existing data structures.
OO code, on the other hand, makes it easy
to add new classes without changing existing functions.

The complement is also true:
Procedural code makes it hard to add new data
structures because all the functions must
change. OO code makes it hard to add new functions because all the classes must change

                            -Robert C Martin
```

## Class
Class adalah *user-defined data type* dan merupakan *fundamental building block* dalam pemrograman berorientasi objek yang berfungsi  sebagai *template/blueprint* yang nantinya akan digunakan untuk menginstansiasi sebuah *object*.

Berikut merupakan contoh pattern sebuah class yang sering dijumpai

```java
package com.example.project;  // Package declaration

import java.util.List;        // Standard imports
import org.apache.commons.*;  // Third-party library imports
import com.example.utils.*;   // Project-specific imports

/**
 * Example class student
 */
public class Student {

    // Constants (static fields)
    public static final int MAX_STUDENT = 100;
    
    // Static variables
    private static int studentCount = 0;

    // Instance variables
    private String name;
    private String dateOfBirth;
    private int age;
    
    // Constructor
    public Student(String name, String dateOfBirth, int age) {
        this.name = name;
        this.age = age;
        this.dateOfBirth = dateOfBirth;
    }

    // Public methods
    public void displayDetails() {
        System.out.println("Name: " + name + ", Age: " + age + ", DOB: " + dateOfBirth);
    }

    // Private methods
    private void validateAge() {
        if (age < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
        }
    }

    // Getters and Setters
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

```


## Object
*Object* merupakan *instance* dari sebuah *class*. Dalam OOP, *object* merepresentasikan entitas dunia nyata yang memiliki atribut (*properties*) dan perilaku (*methods*). *properties* menggambarkan sifat dari *object*, sementara *methods* adalah tindakan yang dapat dilakukan oleh object.

```java
class MyClass {
  public static void main(String[] args) {
    Student anys = new Student("anys", "09-11-2001", 20);
    Student rega = new Student("rega", "09-12-2004", 21);
    anys.age = 19;
    rega.getName();
  }
}
```

## Method
*Method* adalah sebuah *function* yang ada di dalam sebuah class untuk menjalankan sebuah fungsi tertentu. *Method* bisa menerima parameter sebagai *input*, melakukan operasi, dan me-*return* hasil (*output*). *Method* adalah cara bagi sebuah *object* untuk berinteraksi melakukan sesuatu.

Misalkan kita memiliki sebuah kalkulator. Kalkulator tersebut memiliki sebuah cara (*method*) untuk menjumlahkan dua buah bilangan. Maka berikut merupakan contoh kasar dari *function* yang dimiliki oleh kalkulator tersebut :

```java
public class Calkulator {
    // Simple Method example
    public int addition(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        Calkulator calkulator = new Calculator();
        
        System.out.println("Method 1: " + Calculator.addition(5, 10));
    }
}
```

Pada contoh *Calculator class* sederhana di atas, pemanggilan sebuah *method* dilakukan dengan cara menggunakan **Dot Operator**, yaitu . (titik) setelah nama *object* atau *class* yang dilanjutkan dengan nama *method* yang ingin dipanggil.



### Method Overloading
*Method Overloading* adalah sebuah fitur pada Java untuk membuat beberapa *method* dengan nama yang sama, tetapi dengan parameter yang berbeda (baik jumlah, tipe, atau urutannya). Tujuannya adalah untuk menyediakan cara yang fleksibel dalam menjalankan suatu *method* yang mirip, tapi dengan input yang berbeda.

Beberapa hal yang perlu diingat tentang method overloading:
- Nama yang Sama: *Method-method* dalam *method-overloading* harus memiliki nama yang sama.
- Parameter yang Berbeda: Setiap *method* dalam overloading harus memiliki parameter yang berbeda seperti berbeda dalam jumlah parameter, tipe parameter, atau keduanya.
- Tipe Parameter: Tipe parameter yang berbeda dapat mencakup perbedaan dalam urutan tipe data, jumlah tipe data, atau keduanya.
- Tidak Bergantung pada *Return Type*: *Compiler* hanya mempertimbangkan parameter saat memutuskan *method* mana yang harus dijalankan. *Return type* tidak mempengaruhi pemilihan metode.

```java
public class Calkulator {
    // Method with 2 input
    public int addition(int a, int b) {
        return a + b;
    }

    // Method with 2 input
    public int addition(int a, int b, int c) {
        return a + b + c;
    }

    // Method with 2 decimal input
    public double addition(double a, double b) {
        return a + b;
    }

    public static void main(String[] args) {
        Calkulator calkulator = new Calkulator();
        
        System.out.println("Method 1: " + Calkulator.addition(5, 10)); // 15
        System.out.println("Method 2: " + Calkulator.addition(5, 10, 15)); // 30
        System.out.println("Method 3: " + Calkulator.addition(2.5, 3.5)); // 6.0
    }
}
```
Dalam contoh *method overloading* di atas, *class Calkulator* memiliki tiga *method* yang memiliki nama yang sama (*addition*) tetapi berbeda dalam hal jumlah parameter dan tipe parameter. *Compiler* akan memutuskan *method* mana yang harus dijalankan berdasarkan parameter yang diberikan saat memanggilnya.

### varargs parameter

```java
public void printName(String... names) {
    for (String name : Names) {
        System.out.println(name);
    }
}
```
*Variable-length arguments*, merupakan fitur *parameter passing* dari Java untuk mem-*passing argument* dalam jumlah yang bervariasi hingga tak terbatas pada sebuah *function*. Beberapa poin penting pada varargs :

1. Diperlakukan sebagai **Array**.
2. Penempatan varargs **harus** terletak pada parameter terakhir.
   
## Package
*Package* adalah sebuah mekanisme untuk mengorganisir dan mengelompokkan class-class (*classes*) dan antarmuka (*interfaces*) ke dalam hierarki yang terstruktur. Tujuannya adalah untuk membantu developer mengatur kode program mereka dengan testruktur, mencegah konflik nama, dan memudahkan penggunaan *classes* yang sudah ada.

### Struktur Package
*Package* adalah direktori yang mengandung *file-file class Java*. Nama package biasanya dimulai dengan domain terbalik (misalnya, com.example.project) untuk menghindari tabrakan nama dengan package lain.

### Import Package
Untuk menggunakan *class* dari *package* lain, kita perlu mengimpornya menggunakan *keyword import*. Gunakan *wildcard* untuk meng*import* semua kelas dalam sebuah *package*. Misalnya, ```import sampel.*``` akan meng*import* semua *class* dalam paket ```sampel```.

```java
// Import class ArrayList from package java.util
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // Using ArrayList from package java.util
        ArrayList<String> humanList = new ArrayList<>();
        humanList.add("Alice");
        humanList.add("Bob");
        System.out.println(humanList);
    }
}
```
Contoh code di atas menggunakan class ArrayList dari mengimport package java.util.ArrayList. Penggunaan package membantu menjaga kode program besar tetap teratur dan mudah dikelola serta membuat kode kita menjadi bentuk yang lebih terstruktur dan modular.

## Constructor

```java
public class Karyawan {
    // Class Properties
    String nama;
    int usia;

    // Constructor without parameter
    public Karyawan() {
        nama = "Belum Diketahui";
        usia = 0;
    }

    // Constructor with parameter
    public Karyawan(String nama, int usia) {
        this.nama = nama;
        this.usia = usia;
    }

    public void tampilkanInfo() {
        System.out.println("Nama: " + nama);
        System.out.println("Usia: " + usia + " tahun");
    }

    public static void main(String[] args) {
        // Obj
        Karyawan karyawan1 = new Karyawan();

        // Membuat objek Karyawan dengan constructor dengan parameter
        Karyawan karyawan2 = new Karyawan("Alice", 30);

        // Memanggil metode untuk menampilkan informasi karyawan
        karyawan1.tampilkanInfo();
        karyawan2.tampilkanInfo();
    }
}
```
Constructor adalah method khusus dalam sebuah kelas yang digunakan untuk menginisialisasi objek dari kelas tersebut. Constructor memiliki beberapa karakteristik yang membedakannya dari method biasa:

1. memiliki nama yang sama dengan nama class. 
2. tidak memiliki return type (void). 
3. dipanggil secara otomatis saat objek dibuat.
   
Dalam contoh code di atas terdapat dua constructor, satu tanpa parameter dan satu dengan parameter. Kedua constructor digunakan untuk menginisialisasi objek Karyawan dengan argument yang sesuai.
